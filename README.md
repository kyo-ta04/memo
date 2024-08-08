# ASCIIART (マンデンブロ集合) のソース
## MSBASIC (実数型)
全てはここから
```
10 FOR Y=-12 TO 12
20 FOR X=-39 TO 39
30 CA=X*0.0458
40 CB=Y*0.08333
50 A=CA
60 B=CB
70 FOR I=0 TO 15
80 T=A*A-B*B+CA
90 B=2*A*B+CB
100 A=T
110 IF (A*A+B*B)>4 THEN GOTO 200
120 NEXT I
130 PRINT " ";
140 GOTO 210
200 IF I>9 THEN I=I+7
205 PRINT CHR$(48+I);
210 NEXT X
220 PRINT
230 NEXT Y
```

## TinyBASIC (整数型)
ASCIIARTに不可能はない！
```
10 F=50
20 Y=-12
30 X=-39
40 C=X*229/100
50 D=Y*416/100
60 A=C
70 B=D
80 I=0
90 Q=B/F
95 S=B-Q*F
100 T=(A*A-B*B)/F+C
110 B=2*(A*Q+A*S/F)+D
120 A=T
121 P=A/F
122 Q=B/F
123 Z=0
124 IF (P*P+Q*Q)<5 GOTO 150
125 IF I=0 PRINT "0",
126 IF I=1 PRINT "1",
127 IF I=2 PRINT "2",
128 IF I=3 PRINT "3",
129 IF I=4 PRINT "4",
130 IF I=5 PRINT "5",
131 IF I=6 PRINT "6",
132 IF I=7 PRINT "7",
133 IF I=8 PRINT "8",
134 IF I=9 PRINT "9",
142 IF I=10 PRINT "A",
143 IF I=11 PRINT "B",
144 IF I=12 PRINT "C",
145 IF I=13 PRINT "D",
146 IF I=14 PRINT "E",
147 IF I=15 PRINT "F",
148 Z=-1
149 GOTO 245
150 I=I+1
155 IF I<16 GOTO 245
160 PRINT " ",
170 Z=-1
245 IF Z=0 GOTO 90
250 X=X+1
255 IF X<=39 GOTO 40
260 PRINT
270 Y=Y+1
275 IF Y<=12 GOTO 30
280 PRINT "OK"
```

## Common Lisp (実数型)
MSBASICのものから移植
```
(loop for y from -12 to 12 do
  (loop for x from -39 to 39 do
    (let* ((ca (* x 0.0458))
           (cb (* y 0.08333))
           (a ca)
           (b cb)
           (i 0)
           (escaped nil))
      (loop while (and (< i 16) (not escaped)) do
        (let ((temp (+ (- (* a a) (* b b)) ca)))
          (setf b (+ (* 2 a b) cb))
          (setf a temp)
          (if (> (+ (* a a) (* b b)) 4)
              (setf escaped t)))
        (incf i))
      (if escaped
          (if (> i 9)
              (princ (code-char (+ 48 (+ i 7))))
              (princ (code-char (+ 48 i))))
          (princ " "))))
  (terpri))
```

## FORTH (整数型)
TinyBASICのものから移植、CP/M 8080 figFORTH 1.1/1.3, Z80 figFORTH 1.1g で試しました
```
0 VARIABLE Y　0 VARIABLE X　0 VARIABLE C
0 VARIABLE D　0 VARIABLE A　0 VARIABLE B
0 VARIABLE Z　0 VARIABLE T　0 VARIABLE F
0 VARIABLE Q　0 VARIABLE S　0 VARIABLE P
0 VARIABLE II

: OUTCH
  II @ 10 < IF
    II @ 48 + EMIT
  ELSE
    II @ 15 > IF
     32 EMIT
    ELSE
      II @ 55 + EMIT
    THEN
   THEN
; 

: RUN
  CR
  50 F !
  13 -12 DO I Y !
    40 -39 DO I X !
      X @ 229 * 100 / C !
      Y @ 416 * 100 / D !
      C @ A !
      D @ B !
      0 II !
      BEGIN
        B @ F @ / Q !
        B @ Q @ F @ * - S !
        A @ A @ * B @ B @ * - F @ / C @ + T !
        2 A @ Q @ * A @ S @ * F @ / + * D @ + B !
        T @ A !
        A @ F @ / P !
        B @ F @ / Q !
        0 Z !
        P @ P @ * Q @ Q @ * + 4 > IF
          OUTCH
          -1 Z !
        ELSE
          II @ 1 + II !
          II @ 15 > IF
              32 EMIT
              -1 Z !
          THEN
        THEN
        Z @ -1 =
      UNTIL
    LOOP
    CR
  LOOP
  ." OK" CR QUERY QUERY
;
```

## C (実数型)
Hi-TECH C Z80 v3.09 CP/M-80 2.2 で試しました  
```
/*
cpm c asciiart.c -LF
*/

#include <stdio.h>

char	junk[256];

main()
{
	int i, x, y;
	float a, b, ca, cb, t;

	printf("hit Enter key:");
	gets(junk);

	for (y = -12; y <= 12; y++) {
		for (x = -39; x <= 39; x++) {
			ca = x * 0.0458;
			cb = y * 0.08333;
			a = ca;
			b = cb;
			for (i = 0; i <=15; i++) {
				t = a * a - b * b + ca;
				b = 2 * a * b + cb;
				a = t;
				if ((a * a + b * b) > 4) {
					break;
				}
			}
			putch("0123456789ABCDEF "[i]);
		}
		putch('\n');
	}
	printf("OK\n");
	printf("hit Enter key:\n");
	gets(junk);
}
```

## Turbo Pascal (実数型)
Turbo Pascal v3.01a CP/M-80 で試しました  
```
program asciart;

{$C-}

label break;

var
  i,x,y: integer;
  a,b,ca,cb,t: real;
  h: string[16];
  junk: string[255];

begin
  write('Hit Enter key:');
  readln(junk);
  h := '0123456789ABCDEF';

  for y:=-12 to 12 do begin
    for x:= -39 to 39 do begin
      ca := x * 0.0458;
      cb := y * 0.08333;
      a := ca;
      b := cb;
      for i:=0 to 15 do begin
        t := a * a - b * b + ca;
        b := 2.0 * a * b + cb;
        a := t;
        if (a * a + b * b > 4) then
          goto break;
      end;
break:
      write(h[i+1]);
    end;
  end;
  writeln('OK');
  writeln('Hit Enter key:');
  readln(junk);
end.
```
