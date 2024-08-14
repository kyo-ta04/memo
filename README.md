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
100 S=B-Q*F
110 T=(A*A-B*B)/F+C
120 B=2*(A*Q+A*S/F)+D
130 A=T
140 P=A/F
150 Q=B/F
160 Z=0
170 IF (P*P+Q*Q)<5 GOTO 360
180 IF I=0 PRINT "0",
190 IF I=1 PRINT "1",
200 IF I=2 PRINT "2",
210 IF I=3 PRINT "3",
220 IF I=4 PRINT "4",
230 IF I=5 PRINT "5",
240 IF I=6 PRINT "6",
250 IF I=7 PRINT "7",
260 IF I=8 PRINT "8",
270 IF I=9 PRINT "9",
280 IF I=10 PRINT "A",
290 IF I=11 PRINT "B",
300 IF I=12 PRINT "C",
310 IF I=13 PRINT "D",
320 IF I=14 PRINT "E",
330 IF I=15 PRINT "F",
340 Z=-1
350 GOTO 410
360 I=I+1
370 IF I<16 GOTO 410
380 PRINT " ",
390 Z=-1
410 IF Z=0 GOTO 90
420 X=X+1
430 IF X<=39 GOTO 40
440 PRINT
450 Y=Y+1
460 IF Y<=12 GOTO 30
```

## EXCEL VBA (整数型)
Microsoft Excel 2019で試しました。
```
Sub Macro1()
    Dim F, Y, X, C, D, A, B, I, Q, S, T, P, Z As Integer
    
    F = 50
    Y = -12
    Do
        X = -39
        Do
            C = X * 229 / 100
            D = Y * 416 / 100
            A = C
            B = D
            I = 0
            Do
                Q = B / F
                S = B - Q * F
                T = (A * A - B * B) / F + C
                B = 2 * (A * Q + A * S / F) + D
                A = T
                P = A / F
                Q = B / F
                Z = 0
                If P * P + Q * Q > 4 Then
                     Cells(Y + 13, X + 40).Value = Hex$(I)
                     Z = -1
                Else
                     I = I + 1
                     If I > 15 Then
                        Cells(Y + 13, Y + 40).Value = " "
                        Z = -1
                    End If
                End If
            Loop Until Not (Z = 0)
            X = X + 1
        Loop Until (X > 39)
        Y = Y + 1
    Loop Until (Y > 12)
End Sub
```

## XLISP (整数型)
TinyBASICのものから移植、 XLISP v1.1 CP/M-80 2.2 で試しました。
```
(defun mandel ()
   (fgets)
   (fgets)
   (setq F 50)
   (setq Y -12)
   (while (<= Y 12)
     (setq X -39)
     (while (<= X 39)
       (setq C (/ (* X 229) 100))
       (setq D (/ (* Y 416) 100))
       (setq A C)
       (setq B D)
       (setq I 0)
       (setq Z 0)
       (while (== Z 0)
         (setq Q (/ B F))
         (setq S (- B (* Q F)))
         (setq TT (+ (/ (- (* A A) (* B B)) F) C))
         (setq B (+ (* 2 (+ (* A Q) (/ (* A S) F))) D))
         (setq A TT)
         (setq P (/ A F))
         (setq Q (/ B F))
         (setq Z 0)
         (cond ((> (+ (* P P) (* Q Q) ) 4)
             (cond ((< I 10) (princ I))
               (t (princ (chr (+ 55 I)))))
             (setq Z -1))
           (t (setq I (+ I 1))
             (cond ((> I 15)
	         (princ " ") (setq Z -1))))))
       (setq X (+ X 1)))
     (princ "\n")
     (setq Y (+ Y 1)))
   (princ "OK\n")
   (fgets)
   (princ "")
)
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
0 VARIABLE Y
0 VARIABLE X
0 VARIABLE C
0 VARIABLE D
0 VARIABLE A
0 VARIABLE B
0 VARIABLE Z
0 VARIABLE T
0 VARIABLE F
0 VARIABLE Q
0 VARIABLE S
0 VARIABLE P
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
  ." OK" CR FIRST 80 EXPECT CR
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
