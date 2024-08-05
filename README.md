## ASCIIART マンデンブロ集合 Forth

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
  ." OK" CR QUERY QUERY
;

