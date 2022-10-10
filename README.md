# microcontroller-
Study of 8051 microcontroller and square wave generation
$NOMOD51
$include (c8051f340.inc) ; Include register definition file.
;-----------------------------------------------------------------------------
; EQUATES
;-----------------------------------------------------------------------------
;GREEN_LED equ P2.2 ; Green LED: ‘1’ is ON
;-----------------------------------------------------------------------------
; RESET and INTERRUPT VECTORS
;-----------------------------------------------------------------------------
; Reset Vector
cseg AT 0
ljmp Main ; Locate a jump to the start of
; code at the reset vector.
;-----------------------------------------------------------------------------
; CODE SEGMENT
;-----------------------------------------------------------------------------
Blink segment CODE
rseg Blink ; Switch to this code segment.
Using 0 ; Specify register bank for the
; following program code.

Main:
; Disable the WDT.
Anl PCA0MD, #NOT(040h) ; clear Watchdog Enable bit

; Enable the Port I/O Crossbar
mov XBR1, #40h ; enable Crossbar
orl P2MDOUT, #0CH ; make LED pin output push-pull
orl P2MDIN, #0CH ; make LED pin input mode digital

; Initialize LED to OFF
                         clr P2.2
AGAIN1:      setb P2.2
	       ;setb P2.3
	      ACALL DELAY
	      clr P2.2
	    ACALL DELAY
		                                                              SJMP AGAIN1
                                                                 DELAY: MOV R2, #07H
                                           
                                           AGAIN: MOV R1, #0FFH
                                 HERE: DJNZ R1, HERE
                                   DJNZ R2, AGAIN
                                     MOV R3, #061H    
	                          	 HERE2: DJNZ R3, HERE2	   			
                                 RET
                                 END

In Delay subroutine, there are 3787.87 machine cycles
