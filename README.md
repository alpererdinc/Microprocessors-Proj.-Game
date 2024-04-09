# La Cassembly de Papel: A Password Game

  LCDP is a game in which you will try to find the correct password of the Money Safe in 3 difficulties.

  It's a password game written in Assembly Language. This project is a Microprocessors Course Project (P4) of these students from Cukurova University for Assoc. Prof. Dr. Mustafa Berkan BİÇER's course: 
  Mahmut BUT, Galip DİLER, Fatma Nur GENÇDOĞAN, Alper ERDİNÇ

## Problem Definition

  We wanted to make a safe password cracking game. For this, we needed a menu that directs the user, a system that receives a number from the user and recognizes whether this number matches a random password that 
 only the program knows. At the same time, we wanted to give separate input rights for each digit in the password. And the user should have 5 tries for each entry. We had to strive to make the game have a 
 friendly language and an easy interface. The game required 3 difficulty levels and separate code blocks for each.

## The Procedure

  We thought a lot and exchanged ideas to find the game idea. We finally found the type of game that suits us best. We discussed the problems at hand among ourselves, and tried and failed many times in our search 
 for solutions. We solved those 5 tries by creating a counter in the Emulator, and we used LEDs to hold the user's current number input. In this way, we wrote a game code that uses both the output screen and the LED display screen of the assembly language and Emu8086. 

## How To Play

 - First you must run the code in the assembly program you are using. We are using Emu806.
 - After the program runs, you will see some commands. The game will ask you to choose option number 1, the password you want to find will be 1-digit. If you choose option number 2, it will be 2-digit and if you choose option number 3 the password will be 3-digit. When you choose one of the three, the program will ask you to enter a value to find the digits of this number.
 - You have max 5 guess.
 - All you have to do is say a digit contained in the number. You don't need to find out where it is.
 - You can finish the game or continue playing for more money.
 - If you guess all the numbers correctly, you can reach the money in the safe. Of course, it's up to you to outrun the cops.

## Built With

 - Emu8086 Assembly Language

## Assembly Code
ORG 100h         ;The starting adress of the program (for order flow )
                 
            
.DATA            ;Data partition 

Title1 DB "==== Welcome! This is La cAssembly de Papel! ====$"  ;
                                                                ;Introductory texts of the program 
Title2 DB "==== Find the password, get the money! ====$"        ;

Diff0 DB " Choose Difficulty:$"                   ; Selecting difficulty

Diff1 DB "1. Single Digit Password (EASY)$"       ;Have 3 options:
                                                  ;option1: single digit password (easy one) 
Diff2 DB "2. Two-Digit Password (MEDIUM)$"        ;option2: two-digit password    (medium one)
                                                  ;option3: thress-digit password (hard one) 
Diff3 DB "3. Three-Digit Password (HARD)$"        ;
   
Mid DB "Let's crack the Safe's Password$"         ;

Win1 DB "Congrats! You are a millionaire now.$"    ;If you crack the case in right way

Win2 DB "Great job but stay safe for a while, okay? I hear police sirens...$" ;Celebrating   
                                               ;If you can't crack the case to the safe 
Lose1 DB "Oops! The safe locked permanently. " ;(until you run out of lives)                       

Lose2 DB "Cops are on the way. Go offline and leave the place... NOW!" ;

Restart DB "Or play again? (1. Yes, sure. 2. No way):  $" ;Replay option text 

WrongMSG DB "You entered invalid number.$"  ;For wrong number
 
                     
;;;;; for gamemechs ;;;  

                     
OneSlot DB "_$"                 ;A slot 

TwoSlots DB "_ _$"              ;Two slots

ThreeSlots DB "_ _ _$"          ;Three slots 

EnterNum DB "Enter a number: $" ;Number entry request  

FourSlot2 DB "4 _$"             ;Text for four-slot case           

FourSeven2 DB "4 7$"            ;Text for complete case 

SlotSeven2 DB "_ 7$"            ;Text for slot-seven case    

Nine1 DB "9$"                           ;Text for nine case 

FiveSlotSlot DB "5 _ _$"                ;Text for Five-Slot-Slot case

FiveFiveSlot DB "5 5 _$"                ;Text for Five-Five-slot case
                       
FiveFiveFive DB "5 5 5$"                ;Text for Five-Five-Five case         

Message DB "You couldn't find it :( $"  ;Message to be displayed when the game ends  

5Tries DB "You have 5 attempts to enter a wrong number.$"; Message giving the user 5 attempts to achieve    
                                                            
GameOver DB "===== Game Over =====$" ;"Game Over" message displayed at the end of the game
                       
.CODE       

                        
MOV AX, @DATA             ;Put the data part in AX register 
MOV DS, AX                ;Then go to data Seg

#start=led_display.exe#   ;Reset the LED

MOV AX, 0                 ;Reset AX
    
OUT 199,AX                ;Send AX value to port 199
    
;Display Title1  
    CALL NewLine              ;Call the Newline Label  (at the bottom)
    
    MOV DX, offset Title1     ;Getting address of 'Title1' variable on DX
    MOV AH, 09h               ;Assign the write function to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation 
    
    CALL NewLine              ;Call NewLine 
    
;Display Title2
    MOV DX, offset Title2     ;Getting address of 'Title2' variable on DX
    MOV AH, 09h               ;Assign the write function to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation 
    
    CALL NewLine              ;Call NewLine 

;;;; main loop ;;;

Start:

    CALL NewLine              ;Call NewLine 
                  
;Display Diff0             
    MOV DX, offset Diff0      ;Assign memory address of 'Diff0' data to DX register  
    MOV AH, 09h               ;Assign the write function to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call NewLine 
    
;Display Diff1
    MOV DX, offset Diff1      ;Assign memory address of 'Diff1' data to DX register  
    MOV AH, 09h               ;Assign the write function to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
                            
    
    CALL NewLine              ;Call NewLine 
    
;Display Diff2
    MOV DX, offset Diff2      ;Assign memory address of 'Diff2' data to DX register 
    MOV AH, 09h               ;Assign the write function to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation 
    
    CALL NewLine              ;Call NewLine 
    
;Display Diff3
    MOV DX, offset Diff3      ;Assign memory address of 'Diff3' data to DX register  
    MOV AH, 09h               ;Assign the write function to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation 
    
;Get number input
    MOV AH, 01h               ;Place (01h)in AH
    INT 21h                   ;Call the '21h'interrupt to get the character from the keyboard
    MOV BH, AL                ;Assign the first digit of the number to BH 
    
    CALL NewLine              ;Call NewLine 
                
    
    
    CMP BH, '1'               ;Go to input level 1 
    JE OneDigitGame   
    
    CMP BH, '2'               ;Go to input level  2 
    JE TwoDigitGame  
    
    CMP BH, '3'               ;Go to input level 3 
    JE ThreeDigitGame    
    
    JMP WrongNum              ;If something not 1,2,3 is entered go there

WrongNum:

    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call NewLine 
                   
    MOV DX, offset WrongMSG   ;Invalid input message
    MOV AH, 09h               ;Assign the write function to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    JMP Start                 ;Jump back to Label 'Start' if reached  
 
 ;;;Easy mode ;;
  
OneDigitGame:
      
;Display Mid
    MOV DX, offset Mid        ;Get memory adress of variable 'Mid' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call Newline again
    
    MOV DX, offset 5Tries     ;Get memory address of variable '5Tries' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
          
Slot1: 

    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    MOV DX, offset OneSlot    ;Assign address pointing to a slot to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline  
    
    MOV DX, offset EnterNum   ;Show text " Enter a number:"
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
;Get number input
    MOV AH, 01h               ;Place (01h)in AH
    INT 21h                   ;Call the '21h'interrupt to get the character from the keyboard
    MOV BH, AL                ;Assign the first digit of the number to BH
    
    MOV [088h],BH             ;Move the value of BH to memory address  [088h]
    CALL InputToLED           ;Call the InputToLED
    
    CMP BH,057                ;Compare BH with '057'  (9)
    JE One1                   ;If is equal go to 'One1' tag 
     
    CALL Counter              ;Call the counter 
    JMP Slot1                 ;Jump the Slot1 tag 

One1: 
   
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
;Display Mid
    MOV DX, offset Nine1      ;Move memory address of variable 'Nine1' to DX 
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline again
    
    MOV DX, offset 5Tries     ;Move memory address of variable '5Tries' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    JE WinEnd                 ;If it's equal go to 'WinEnd' 
    
    JMP LoseEnd               ;Otherwise go to 'LoseEnd'  
    

;;; Medium mode ;;;
     
TwoDigitGame:

;Display Mid
    MOV DX, offset Mid        ;Get memory address of variable 'Mid' to DX 
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call Newline 
    
    MOV DX, offset 5Tries     ;Get memory address of variable '5Tries' to DX 
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
               
               
    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call Newline 
     
TwoZero:
     
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
          
    MOV DX, offset TwoSlots   ;Show 'TwoSlots' 
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
           
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
     
    MOV DX, offset EnterNum   ;Show text " Enter a number:"
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    
;Get number input
    MOV AH, 01h               ;Place (01h)in AH
    INT 21h                   ;Call the '21h'interrupt to get the character from the keyboard
    MOV BH, AL                ;Assign the first digit of the number to BH  
    
    MOV [088h],BH             ;Move the value of BH to memory address  [088h]
    CALL InputToLED           ;Call the InputToLED
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
     
    CMP BH,052                ;Compare with 4 
    JE TwoOne                 ;If it's 4 go to 'TwoOne'
    
    CMP BH,055                ;Compare with 7 
    JE TwoTwo                 ;If it's 7 go to 'TwoTwo'
                       
    CALL Counter
              
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    JMP TwoZero               ;The case with first slot is correct
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
            
TwoTwo:

    MOV DX, offset SlotSeven2 ;Show the seven-slot password 
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
                
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    MOV DX, offset EnterNum   ;Show text " Enter a number:"
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation 
    
;Get number input
    MOV AH, 01h               ;Place (01h)in AH
    INT 21h                   ;Call the '21h'interrupt to get the character from the keyboard
    MOV BH, AL                ;Assign the first digit of the number to BH 
    
    MOV [088h],BH             ;Move the value of BH to memory address  [088h]
    CALL InputToLED           ;Call the InputToLED
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    
                             
    CMP BH,052                ;Compare with 4 
    JE  TwoOneTwo             ;If it's 4 go to 'TwoOneTwo
    
    CALL Counter
    
    JMP TwoTwo                ;Otherwise go to 'TwoTwo'

TwoOne: 


    MOV DX, offset FourSlot2  ;Show the four slot password 
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    MOV DX, offset EnterNum
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation 
    
;Get number input
    MOV AH, 01h               ;Place (01h)in AH
    INT 21h                   ;Call the '21h'interrupt to get the character from the keyboard
    MOV BH, AL                ;Assign the first digit of the number to BH  
    
    MOV [088h],BH             ;Move the value of BH to memory address  [088h]
    CALL InputToLED           ;Call the InputToLED
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
     
    CMP BH,055                ;Compare with 7 
    JE TwoOneTwo              ;If it's 7 go to 'TwoOneTwo'
    
    CALL Counter
    
    JMP TwoOne                ;Otherwise go to 'TwoOne'

TwoOneTwo:            

    MOV DX, offset FourSeven2 ;Show the password        
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
       
                                
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
                                
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
     
    JE WinEnd                 ;If it's true go to 'WinEnd'
    
    JMP LoseEnd               ;Otherwise go to 'LoseEnd'  

 ;;;; Hard mode ;;;; 

ThreeDigitGame:

;Display Mid
    MOV DX, offset Mid        ;Get memory address of variable 'Mid' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    MOV DX, offset 5Tries     ;Assign the address '5Tries' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
               
SlotSlotSlot:

    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
      
    MOV DX, offset ThreeSlots ;Assign the address showing the three-slot password to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
                
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
               
    MOV DX, offset EnterNum   ;Show text " Enter a number:"
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
;Get number input
    MOV AH, 01h               ;Place (01h)in AH
    INT 21h                   ;Call the '21h'interrupt to get the character from the keyboard
    MOV BH, AL                ;Assign the first digit of the number to BH 
    
    MOV [088h],BH             ;Move the value of BH to memory address  [088h]
    CALL InputToLED           ;Call the InputToLED
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    CMP BH, 053               ;Compare BH to '053' ('5' in ASCII)     
    JE ThreeSlotSlot          ;If it's equal go to 'ThreeSlotSlot' tag 
    
    CALL Counter              ;Call the counter routine 
    
    JMP SlotSlotSlot          ;Go to 'SlotSlotSlot' tag 

ThreeSlotSlot: 

    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call Newline 
    
    MOV DX, offset FiveSlotSlot ;Move memory address of 'FiveSlotSlot' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;nterrupt that performs the write operation
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
               
    MOV DX, offset EnterNum   ;Show text " Enter a number:"
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;interrupt that performs the write operation
    
    ;Get number input
    MOV AH, 01h               ;Place (01h)in AH
    INT 21h                   ;Call the '21h'interrupt to get the character from the keyboard
    MOV BH, AL                ;Assign the first digit of the number to BH
    
    MOV [088h],BH             ;Move the value of BH to memory address  [088h]
    CALL InputToLED           ;Call the InputToLED
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    CMP BH, 053               ;Compare BH to '053' ('5' in ASCII)     
    JE ThreeThreeSlot         ;If it's equal go to 'ThreeThreeSlot' tag
    
    CALL Counter              ;Call the counter routine
    
    JMP ThreeSlotSlot         ;Go to 'ThreeSlotSlot' tag
               
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 

ThreeThreeSlot: 
 
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
               
    MOV DX, offset FiveFiveSlot ;Move memory address of 'FiveFiveSlot' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
               
    MOV DX, offset EnterNum   ;Show text " Enter a number:"
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
;Get number input
    MOV AH, 01h               ;Assign a value to AH for reading characters from the keyboard 
    INT 21h                  
    MOV BH, AL                ;Move value from AL to BH
    
    MOV [088h],BH             ;Move the value of BH to memory address  [088h]
    CALL InputToLED           ;Call the InputToLED
    
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    CMP BH, 053               ;Compare BH to '053' ('5' in ASCII) 
    JE ThreeThreeThree        ;If it's equal go to 'ThreeThreeThree' tag
    
    CALL Counter              ;Call the counter routine 
    
    
    JMP ThreeThreeSlot        ;Go to 'ThreeThreeSlot' tag 
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
            
ThreeThreeThree:            
            
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
                 
    MOV DX, offset FiveFiveFive ;Move memory address of 'FiveFiveFive' to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline   
    CALL NewLine              ;Call Newline 
    
    JE WinEnd                 ;If correct number entered go to 'WinEnd'
    
    JMP LoseEnd               ;If wrong number entered go to 'LoseEnd' 


WinEnd:
                   
;Display Win1
    MOV DX, offset Win1       ;Get memory address of variable 'Win1' and assign it to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline  
                       
    ;Display Win2
    MOV DX, offset Win2       ;Get memory address of variable 'Win2' and assign it to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
                           
    JMP RES                   ;Go to 'RES' Tag 
    
LoseEnd:
                   
;Display Lose1
    MOV DX, offset Lose1      ;Get memory address of variable 'Lose1' and assign it to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    CALL NewLine              ;Call Newline 
                       
;Display Lose2
    MOV DX, offset Lose2      ;Get memory address of variable 'Lose2' and assign it to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
    JMP RES                   ;Go to 'RES' Tag 
      
RESfail:                      ;Actions taken in case of error 

    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    
    MOV DX, offset Message    ;Move memory address of 'Message' variable to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
            
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
        
RES:                                   

    CALL resCount
    CALL NewLine              ;Call Newline 
;Display Restart
    MOV DX, offset Restart    ;Get memory address of variable 'Restart' and assign it to DX
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Interrupt that performs the write operation
    
;Get number input
    MOV AH, 01h               ;Upload '01h' to AH to read it from the keyboard 
    INT 21h                   ;Interrupt '21h' call to get character from user         
    MOV BH, AL                ;Assign the first digit of the number to BH 
     

CMP BH, '1'             ;Check if the character entered by the user is '1'
JE Start                ;Get back to 'Start' tag 

CMP BH, '2'
JE EndGame              ;If user entered a character other than '1' go to Endgame tag

JMP WrongNum            ;Go to 'WrongNum' tag when there is an incorrect number 
         


NewLine:    
             
    MOV DL, 13                ;Assign newline character (13) to DL
    MOV AH, 02h               ;Assign printing to AH (02h)
    INT 21h                   ;Interrupt '21h' call to get character from user
                   
    MOV DL, 10                ;Assign (10) to DL to get to the bottom line  
    MOV AH, 02h               ;Assign printing to AH (02h)                  
    INT 21h                   ;Interrupt '21h' call to get character from user
      
      
    RET                       ;Return from subroutine    
        
resCount:               ;Restart counter 

    MOV CH, 5                 ;Assign CH to '5'
    RET                       ;Return from subroutine 

Counter:                ;Subroutine that decreases the counter 

    DEC CH                    ;Decrease the CH 
    MOV [99h], CH             ;Assign CH to address [99h] in memory 
    CMP CH, 0                 ;Check if CH is 0 
        
        
    JE RESfail                ;If it's 0 go to 'RESfail' tag
        
    RET



InputToLED:             
    
    SUB [088h], '0'           ;Subtract '0' from value address [088h]
    
    MOV AX, [088h]            ;Load value at address [088h] into AX
    
    OUT 199, AX               ;Send AX value to port 199 
               
    RET   

EndGame:                  ;Ending the game  

    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    
    MOV DX, offset GameOver   ;Move memory address of 'GameOver' variable to DX      
    MOV AH, 09h               ;Assign printing to AH (09h)
    INT 21h                   ;Perform printing
    
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline 
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    CALL NewLine              ;Call Newline
    
    
    HLT                       
              

## Developers

- Fatma Nur GENÇDOĞAN,     Alper ERDİNÇ,     Mahmut BUT,     Galip DİLER

## Special Thanks

- Assoc. Prof. Dr. Mustafa Berkan BİÇER for his Microprocessors Course
- Research Assistant A. Abbas ELMAS for his Microprocessors Lab. Course

 


