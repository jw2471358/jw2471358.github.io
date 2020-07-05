---
layout: post
title: WebToB CGI C, Perl 예제
subtitle: 
description: WebToB CGI C, Perl 예제
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/moon-5224745_1920_ufjpll.jpg
category: CGI
tags:
  - WebToB
  - CGI
  - C
  - Perl
author: jw2471358
---

### C를 이용한 게시판 구현

"board.html"에서 "board.cgi"를 호출해서 구현한다

- sample_cgi.m

```
#Configuration file  ( sample_cgi.m )

*DOMAIN
webtob

*NODE
webmain         WEBTOBDIR = "$WEBTOBDIR",
                SHMKEY = 72000, HTH=1,
                DOCROOT = "docs/",
                PORT = "8080"

*SVRGROUP
htmlg           NODENAME = webmain, SvrType = HTML
cgig          NODENAME = webmain, SvrType = CGI 

*SERVER
html            SVGNAME = htmlg, MinProc = 1, MaxProc = 5
cgi           SVGNAME = cgig,  MinProc = 1, MaxProc = 5

*URI
uri1          Uri = "/cgi-bin/", SvrName = cgi, Svrtype = CGI

*ALIAS
alias1        URI = "/cgi-bin/",
              RealPath = "${WEBTOBDIR}/cgi-bin/"
```

- board.html

```html
<HTML>
<HEAD><TITLE>WebToB Board</TITLE></HEAD>
<BODY>
<H2><big>WebToB Board Upload</big></H2>
<HR WIDTH=500 ALIGN=left><BR>
<FORM METHOD=post ACTION="/cgi-bin/board.cgi">
<TABLE WIDTH=500 BORDER=0>
 <TR>
     <TD>Writer</TD>
     <TD><INPUT NAME=writer SIZE=20></TD>
</TR>
<TR>
     <TD>Title</TD> 
     <TD><INPUT NAME=title SIZE=50></TD>
</TR>
<TR>
     <TD COLSPAN=2><B>Contents</B></TD>
</TR>
<TR>
     <TD COLSPAN=2>
     <TEXTAREA NAME=doc COLS=60 ROWS=10></TEXTAREA>
     </TD>
</TR>
<TR>
     <TD>E-Mail</TD>
     <TD><INPUT NAME=email SIZE=40></TD>
</TR>
<TR>
     <TD>Home Page</TD>
     <TD>
     <INPUT NAME=homepage
            SIZE=40 VALUE="http://">
     </TD>
</TR>
</TABLE> 
<BR>
<INPUT TYPE=submit VALUE="    Submit    ">
<INPUT TYPE=reset VALUE="     Clear     "> 
</FORM>
</BODY>
</HTML>
```

- board.c

```c
#include "qDecoder.h"

int strcheck(char *str) {
  /* 문자열이 NULL이거나 길이가 0인지 체크 */
 if (str == NULL)
        return 0;
 if (strlen(str) == 0)
        return 0;
 return 1;
}

int main(void) {
  char *name, *title, *doc;
  char *email, *homepage;

  /* 입력값들을 얻어냄 */
  name = qValue("writer");
  title = qValue("title");
  doc = qValue("doc");
  email = qValue("email");
  homepage = qValue("homepage");

  /* 입력값들이 올바른지 검사 */
  if (!strcheck(name))
     qError("Type Your Name !");
  if (!strcheck(title))
     qError("Type Title !");
  if (!strcheck(doc))
     qError("Write Your Messages !");
  if (strcheck(email))
    if (!qCheckEmail(email))
       qError("Type Your E-Mail !");
  if (strcheck(homepage))
    if (!qCheckURL(homepage))
       qError("Type Your Homepage URL !");

  /* 여기서 게시판에 추가합니다. */
  /* 처리 결과 출력 - 입력 확인 */
  qContentType("text/html");
  printf("<HTML>\n\n");
  printf("<HEAD><TITLE>CGI Board TEST</TITLE></HEAD>\n\n");
  printf("<BODY>\n");
  printf("<H2> CGI Board TEST </H2>\n");
  printf("<HR WIDTH=600 ALIGN=left>\n<BR>");
  if (strcheck(email))
     printf("<A HREF=\"mailto:%s\">%s</A>",email,name);
  else
     printf("%s", name);

  if (strcheck(homepage))
     printf( "<SMALL>(<A HREF=\"%s\">%s</A>)</SMALL>",
             homepage,
             homepage );

  printf("wrote<BR><BR>\n");
  printf("<TABLE WIDTH=600 BORDER=1>\n");
  printf("<TR><TD><B>Title</B> : %s</TD></TR>\n", title);
  printf("<TR><TD>%s</TD></TR>\n", doc);
  printf("</TABLE>\n\n<BR>Upload Successful !\n");
  printf("</BODY>\n\n</HTML>");
  qFree();
}
```

- 작업 및 결과 확인
1) 환경 파일인 sample_cgi.m을 시스템에 맞게 수정한다.

2) HTML 문서를 DocRoot로 옮긴다.

3) board.html의 ACTION=”/cgi-bin/board.cgi” 부분이 자신의 환경에서 board.cgi가 있는 곳으로 설정한다.

4) board.c 및 qDecoder.h, qDecoder.c를 CGI가 구동되는 디렉터리로 옮긴다.

5) board.c를 컴파일하면 board.cgi가 생성된다(cc 또는 gcc가 설치되어 있어야 한다).

```
$ gcc board.c qDecoder.c –o board.cgi 
$ chmod 755 board.cgi
```

http://localhost:8080/board.html

![placeholder](https://technet.tmaxsoft.com/upload/download/online/webtob/pver-20150203-000001/administrator/resources/figureB_1.png)

"submit" 버튼을 클릭하면 board.cgi가 호출되어 아래와 같이 게시판에 입력된 화면이 생성된다.

![ploaceholder](https://technet.tmaxsoft.com/upload/download/online/webtob/pver-20150203-000001/administrator/resources/figureB_2.png)

-------------------------------------------------------------------

### PERL을 이용한 게시판 구현

- sample_Perl.m

```
#Configuration file ( sample_perl.m )

*DOMAIN
webtob1

*NODE
webmain          WEBTOBDIR = "/usr/local/webtob",
                 SHMKEY = 72000, HTH=1,
                 DOCROOT = "/usr/local/webtob/docs",
                 PORT = "9989"

*SVRGROUP
htmlg            NODENAME = webmain, SvrType = HTML
cgig           NODENAME = webmain, SvrType = CGI 

*SERVER
html             SVGNAME = htmlg, MinProc = 1, MaxProc = 5
cgi            SVGNAME = cgig,  MinProc = 1, MaxProc = 5

*URI
uri1           Uri = "/cgi-bin/", SvrName = cgi, Svrtype = CGI

*ALIAS
alias1         URI = "/cgi-bin/",
               RealPath = "/usr/local/webtob/docs/cgi-bin/"
```

- Perl 스크립트 작성 guestbook.cgi

```Perl
#guestbook.cgi

#!/usr/local/bin/perl

# 기준 URL (보통 홈페이지 주소)
$Base_href      = 'http://webmain.tmax.co.kr:9081/';

# $base_href 를 기준한 이 화일의 path
$Cgi_file       = 'cgi-bin/guestbook.cgi';

# lock 디렉터리 path
$Lock_dir       = 'lock/guestbook';

# BBS 데이타가 담기는 화일
$Bbs_file       = 'book_data';

# 링크할 제목
$Link_name      = 'Back to Home';
# 링크할 URL ($base_href 기준)
$Link_url       = './';   
                                     
# 제목
$Bbs_title      = 'Guest Book'; 

# 관리자 이름
$Bbsmaster_name = 'webtob'; 

# 관리자 email 주소 
$Bbsmaster_email = 'webotb@tmax.co.kr'; 

# 각 메시지의 최대 크기 (byte) (SPAM 방지용)
$Max_msg_size    = 8000; 
$Titlecolor      = '#800080';
$Bgcolor         = '#fafff8';
$Textcolor       = '#000000';
$Linkcolor       = '#401080';

$Bbs_write_title = 'WRITE';
$Bbs_read_title  = 'READ';

$Rem_name        = '';
$Rem_email       = '';
$Rem_msg         = '' .
                   '' .
                   '';

$Btn_write       = 'Send';
$Btn_read_old    = 'Old Message';
$Btn_read_new    = 'New Message';

$Rem_bbs_end     = 'End of Messages';
$Rem_bbs_back    = 'Go Top';

$Bbs_logo        = '';
$Bbs_logo_addr   = 'http://';

$Delimiter       = chr(30);                     
$Prev_num_skip   = 0;

##### main routine #####

&read_file;
&read_form;

if ($ENV{'REQUEST_METHOD'} eq "POST" && $Name ne "" && $Msg ne "" ) {
        &remove_html_tags;     # remove HTML tags
        &new_msg;              # make new BBS msg, use &clock
        &save_msg;             # save BBS msg
}

&show_header;                  # show header
&show_entry_form;              # show BBS entry form
&show_bbs;                     # show BBS msgs
&show_read_form;               # show BBS read form
&show_footer;                  # show footer
exit;

##### sub routines #####
sub read_file {
        open (IN, "$Bbs_file") || &return_error 
             (500, "File open error", "Cannot access BBS file");
        @Bbs = <IN>;
        close (IN);
}

sub read_form {
        %Form = &read_input;

        $Name     = $Form{'name'};
        $Email    = $Form{'email'};
        $Msg      = $Form{'msg'};
        $Num_each = $Form{'num_each'};
        $Num_skip = $Form{'num_skip'};
}

sub remove_html_tags {
        $Name =~ s/\&/\&amp;/g;
        $Name =~ s/\</\&lt;/g;
        $Name =~ s/\>/\&gt;/g;

        $Email =~ s/\&/\&amp;/g;
        $Email =~ s/\</\&lt;/g;
        $Email =~ s/\>/\&gt;/g;

        $Msg =~ s/\&/\&amp;/g;
        $Msg =~ s/\</\&lt;/g;
        $Msg =~ s/\>/\&gt;/g;

        $Msg =~ s/\r\n/\n/g;          # Windows(CR,LF)     -> LF
        $Msg =~ s/\r/\n/g;            # Mac (CR)           -> LF
        $Msg =~ s/\n/<BR>/g;          # LF                 -> <BR>
}

sub new_msg {
        my ($access_time) = &clock;  # get date and time
        my ($new_msg);
        my ($site) = ($ENV{'REMOTE_HOST'} || $ENV{'REMOTE_ADDR'});

# delete msg larger than 4000 byte
        if (length($Msg) >= 4000) {
              $Msg = substr($Msg, 0, 4000);
                if (($Msg =~ tr/[\xA1-\xFE]//)%2 != 0) {
                      chop $Msg;
                  }
        }

        if ($Email !~ /([\w\-]+\@[\w\-+\.]+[\w\-]+)/) {
                $Email = "";   # check valid email address format
        }

          $new_msg = "$Name"        . $Delimiter .  # name
                     "$Email"       . $Delimiter .  # email address
                     "$site"        . $Delimiter .  # ip_address
                     "$access_time" . $Delimiter .  # access time
                     "$Msg"         . "\n";         # message

        @Bbs = ($new_msg, @Bbs);
}

sub save_msg {
        (&filelock ($Lock_dir) eq 'OK') || &return_error 
        ("500", "Lock error", "Too many access or cannot create lock file");

        open (OUT, ">$Bbs_file") || &return_error 
        (500, "File write error", "Cannot access BBS file");
        print OUT @Bbs;
        close (OUT);

        (&fileunlock ($Lock_dir) eq 'OK') || &return_error 
        ("500", "Unlock error", "No lock file exist");
}

sub show_header {
        print "Content-type: text/html\n\n";
        print <<END_OF_HTML;
<HTML>
<HEAD>
          <BASE HREF="$Base_href">
          <TITLE>$bbs_title</TITLE>
</HEAD>
<BODY BGCOLOR="$Bgcolor" TEXT="$Textcolor" LINK="$Linkcolor">
 <P ALIGN="CENTER"><FONT COLOR="$Titlecolor" SIZE="+2">
<B>$Bbs_title</B></FONT>
<br>
<div align="left"><A HREF="$Link_url">$Link_name</A></div>
<P ALIGN="RIGHT">
<HR>
END_OF_HTML
;
}

sub show_entry_form {
        print <<END_OF_HTML;
<a name="write"> </a>

<FONT COLOR="#800080" SIZE="+1">
<B>$Bbs_write_title</B></FONT>
<P>
<FORM ACTION=\"$Cgi_file\" METHOD=\"POST\">
 <B>Name</B> $Rem_name<BR>
<INPUT NAME="name" TYPE="text" SIZE = "40" MAXLENGTH="64">
<P>
<B>Email address</B> (optional) $Rem_email<BR>
<INPUT NAME="email" TYPE="text" SIZE = "40" MAXLENGTH="72">
<P>
<B>Message</B> $Rem_msg<BR>
<TEXTAREA COLS="64" ROWS="10" WRAP="VIRTUAL" NAME="msg">
</TEXTAREA><BR>
<INPUT TYPE="submit" VALUE="$Btn_write ">
</FORM>
<HR>
END_OF_HTML
;
}

sub show_read_form {
        print <<END_OF_HTML;
<font color="#800080" size="+1"><b>$Bbs_read_title</b></font>
<br><br>

<table border="0" cellspacing="10">
<tr valign="top">
        <td>
                 <FORM ACTION=\"$Cgi_file\" METHOD=\"POST\">
                 <INPUT TYPE="submit" VALUE="$Btn_read_old"><br>
        <INPUT TYPE="radio"
                 NAME="num_each"
                 VALUE="5" CHECKED>5 more
                 <INPUT TYPE="radio"
                        NAME="num_each"
                        VALUE="20">20 more
                 <INPUT TYPE="hidden"
                        NAME="num_skip"
                        VALUE="$Prev_num_skip">
                 </FORM>
        </td>
        <td>
                 <FORM ACTION=\"$Cgi_file\" METHOD=\"POST\">
                 <INPUT TYPE="submit" VALUE="$Btn_read_new"><br>
                 <INPUT TYPE="radio"
                        NAME="num_each"
                        VALUE="-5" CHECKED>5 more
                 <INPUT TYPE="radio"
                        NAME="num_each"
                        VALUE="-20">20 more
                 <INPUT TYPE="hidden"
                        NAME="num_skip"
                        VALUE="$Prev_num_skip">
                 </FORM>
        </td>
        <td></td>
        <td></td>
        <td>
                 <FORM ACTION=\"$Cgi_file\" METHOD=\"POST\">
                 <INPUT TYPE="hidden" NAME="num_each" VALUE="top">
                 <INPUT TYPE="submit" VALUE="Go Top">
                 </FORM>
 </td>
        <td></td>
        <td>
                 <FORM ACTION=\"$Cgi_file\" METHOD=\"POST\">
                 <INPUT TYPE="hidden" NAME="num_each" VALUE="all">
                 <INPUT TYPE="submit" VALUE="Show All"><br>
                 (Warning: very long!)
        </FORM>
        </td>
 </tr>
</table>
<hr>
END_OF_HTML
;
}

sub show_bbs {
        local( $bbs_no,
               $serial_no,
               @show_bbs,
               @data,
               $temp_email,
               $temp_msg );

        $bbs_no = $#Bbs + 1;

        unless (defined ($Num_each)) {$Num_each = 5;}
        unless (defined ($Num_skip)) {$Num_skip = 0;}

        if ($Num_each eq "all") {
               $Num_each = $bbs_no - $Num_skip;
        }
        if ($Num_each eq "top") {
               $Num_each = 5;
               $Num_skip = 0;
        }
        if ($Num_skip >= $bbs_no) {
               &show_end_of_bbs;
        }
        if ($Num_skip + $Num_each > $bbs_no) {
               $Num_each = $bbs_no - $Num_skip;
        }
        if ($Num_each < 0 ) {
               $Num_skip = $Num_skip + $Num_each + $Num_each;
               $Num_each = 0 - $Num_each;
               if ($Num_skip < $Num_each) {
                       $Num_skip = 0;
                }
        } else {
               $Prev_num_skip = $Num_skip + $Num_each;   

# skip data at next loading
        }

        $serial_no = $bbs_no - $Num_skip;             
        # first serial No.

        @show_bbs = splice(@Bbs, $Num_skip, $Num_each); 

# displayed msgs
        while (@show_bbs) {
                @data = split (/$Delimiter/, shift(@show_bbs));
# use slice of message file

                print "[ $serial_no ] <B>";
                print shift(@data);  # $Name
                print '</B>';

                if ($temp_email = shift(@data)) {  # $Email
                        print "<<a href=\"mailto:$temp_email\">$temp_email<\/a>>";
                }
                print ' from ';
                print shift(@data);  # $ip_address
                print ' at ';
                print shift(@data);  # $access_time
                print ' <P>';
                $temp_msg = shift(@data);
                $temp_msg =~ s/(http:\/\/)([\w\+\-\/\=\?\.\~\:\&\;\#]+)/
                             <a href=\"$1$2\" target=\"_new">$1$2<\/a>/g;
                $temp_msg =~ s/([\w\-]+\@[\w\-+\.]+[\w\-]+)/
                             <a href=\"mailto:$1">$1<\/a>/g;
                print $temp_msg;  # $msg
                print "\n<HR>\n";

                $serial_no --;  # prepare next serial No.
        }
}

sub show_end_of_bbs {
        print "$Rem_bbs_end";
        print '<P>';
        print "<A HREF=\"$Cgi_file\">$Rem_bbs_back</A>";
        print "<HR>\n";
}

sub show_footer {
        print <<END_OF_HTML;
<A HREF="$Link_url">$Link_name</A>
<HR>
<I>BBS Master : $Bbsmaster_name
 / <A HREF="mailto:$Bbsmaster_email">$Bbsmaster_email</A></I>

<div align="right">
<B><I><A HREF="$Bbs_logo_addr">$Bbs_logo</A></I></B>
</div>

</body>
</html>
END_OF_HTML
;
}

#### other subroutines (shared with other perl cgi) ########
sub read_input {
        local ($buffer, @pairs, $name, $value, %FORM);
        if ($ENV{'REQUEST_METHOD'} =~ /^post$/i) {
                read(STDIN, $buffer, $ENV{'CONTENT_LENGTH'});
        } else {
                $buffer = $ENV{'QUERY_STRING'};
        }
        @pairs = split(/&/, $buffer);
        foreach (@pairs) {
                ($name, $value) = split(/=/, $_);
                $value =~ tr/+/ /;
                $value =~ s/%([a-fA-F0-9][a-fA-F0-9])/pack("C", hex($1))/eg;
                $FORM{$name} = $value;
        }
        return %FORM;
}

sub clock {
        my ($date);

        @days = ('Sun','Mon','Tue','Wed','Thr','Fri','Sat');
        ($sec,$min,$hour,$mday,$mon,$year,$wday,$yday,$isdst) = localtime(time);
        $mon ++;
        if ($hour < 10) { $hour = "0".$hour; }
        if ($min < 10) { $min = "0".$min; }
        if ($sec < 10) { $sec = "0".$sec; }
        $date = "19$year\.$mon\.$mday\.($days[$wday]) $hour\:$min\:$sec";
}

sub return_error {
        my ($status, $keyword, $msg) = @_;
        print "Content-type: text/html\n";
        print "Status: ", $status, " ", $keyword, "\n\n";
        print "<TITLE>CGI program Error</TITLE>\n";
        print "<H1>", $keyword, "</H1>\n";
        print $msg, "\n";
        print "<P>Please contact the webmaster for more information.\n";
        print "<HR>";
        print "<A HREF=\"http://heartkorea.com/\"><I>Guest Book</I></A>";
        exit(1);
}

sub filelock {                  # parameter is filename for lock
        my ($lockdir) = @_;
        mkdir ($lockdir, 0777) && return 'OK';
        -M $lockdir > 3/(24*60) && do {
                rmdir ($lockdir) || return 'FAIL';
        };
        for (1 .. 10) {
                mkdir ($lockdir, 0777) && return 'OK';
                sleep (1);
        }
        return 'BUSY';
}

sub fileunlock {                  
        my ($lockdir) = @_;
        -d $lockdir || return 'FAIL';
        rmdir ($lockdir) && return 'OK';
        return 'FAIL';
}
#### end of program ########################################
```

B.3.3. 작업 및 결과 확인
작업 순서는 다음과 같다.

1) 환경 파일인 sample_perl.m을 시스템에 맞게 수정한다.

2) $which perl로 Perl의 경로를 얻어온다.

3) guestbook.cgi를 편집창을 열어 시스템에 맞게 수정한다.

4) guestbook.cgi를 CGI가 구동되는 디렉터리로 옮기고 permission을 755로 설정한다.

```
$chmod 755 guestbook.cgi
```

5) guestbook.cgi의 데이터를 저장하기 위한 book_data 파일을 생성하고 permission을 666으로 설정한다.

```
$touch book_data
$chmod 666 book_data
```

6) 마찬가지로 lock 디렉터리를 생성하고 permission을 777로 설정한다.

```
$mkdir lock
$chmod 777 lock
```

7) 시스템을 기동한 후 브라우저에서 다음과 같이 요청한다. (IP 주소는 현재 WebtoB가 구동되고 있는 머신의 것을 사용한다)

http://IP address:port/cgi-bin/guestbook.cgi

8) 실행된 화면은 다음과 같다.

- Perl을 이용한 게시판 입력 화면
![placeholder](https://technet.tmaxsoft.com/upload/download/online/webtob/pver-20150203-000001/administrator/resources/figureB_3.png)

위와 같은 방명록 화면이 뜬다면, 요구하는 정보를 간단히 쓴 다음 [Send] 버튼을 클릭해서 방명록에 기록을 남긴다. guest 2가 남긴 말 위에 webtob가 남긴 말이 추가된다. 방문자들이 남긴 글은 book_data 파일에 남는다.

실행된 화면은 다음과 같다.

- Perl을 이용한 게시판 결과 화면
![placeholder](https://technet.tmaxsoft.com/upload/download/online/webtob/pver-20150203-000001/administrator/resources/figureB_4.png)

### References
- webtob cgi 활용 예 <https://technet.tmaxsoft.com/upload/download/online/webtob/pver-20150203-000001/administrator/cgi_sample.html>