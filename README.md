# Tic-Tac-Toe PLC Base
## Project Overview
![enter image description here](https://github.com/youness-el-kabtane/Tic-Tac-Toe-PLC-base/blob/85f854fe1695fc6b6ac11c5b798a898c55422c36/image/Screenshot1.png)
> A simple Tic-Tac-Toe game built using a Siemens PLC and STEP 7. This
> project was built to experiment with STL programming and strengthen my
> automation logic design skills.
## System Architecture
-   CPU: S7-300 (CPU 314C-2 PN/DP)
-   SIMATIC MP 177 6" Touch
## Variables Tables
![enter image description here](https://github.com/youness-el-kabtane/Tic-Tac-Toe-PLC-base/blob/e68015ea32ec1b9fa35ce1e7eab2d7864f791b7e/image/Screenshot2.png)
## Program Description
### FC1
FC1 contains the main game logic written in Structured Control Language (SCL).  
It checks all possible winning combinations for both players:
-   3 horizontal lines
-   3 vertical lines
-   2 diagonal lines

```PASCAL
FUNCTION FC1: VOID

BEGIN

// O Win Detection

Owin := FALSE;

IF 
   (O1 AND O2 AND O3) OR
   (O4 AND O5 AND O6) OR
   (O7 AND O8 AND O9) OR
   (O1 AND O4 AND O7) OR
   (O2 AND O5 AND O8) OR
   (O3 AND O6 AND O9) OR
   (O1 AND O5 AND O9) OR
   (O7 AND O5 AND O3)
THEN
   Owin := TRUE;
END_IF;


// Prevent both players winning
IF Owin THEN
   Xwin := FALSE;
END_IF;

// X Win Detection

Xwin := FALSE;

IF 
   (X1 AND X2 AND X3) OR
   (X4 AND X5 AND X6) OR
   (X7 AND X8 AND X9) OR
   (X1 AND X4 AND X7) OR
   (X2 AND X5 AND X8) OR
   (X3 AND X6 AND X9) OR
   (X1 AND X5 AND X9) OR
   (X7 AND X5 AND X3)
THEN
   Xwin := TRUE;
END_IF;


// Prevent both players winning
IF Xwin THEN
   Owin := FALSE;
END_IF;

END_FUNCTION
```
### OB1
![enter image description here](#)
-   FC1 is called every PLC scan cycle, so the win conditions are continuously evaluated.
- In OB1, a **Clear** button resets the game by setting memory bytes MB0 to MB3 to zero, clearing all grid positions in a single scan cycle.

---
**Author:**  Youness El Kabtane

**Website:**  [younesselkabtane](https://youness-el-kabtane.github.io/site/)

**Version:**  1.0.0

**Made with 💗**

