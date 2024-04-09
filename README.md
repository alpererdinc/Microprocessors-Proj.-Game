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

## Developers

Fatma Nur GENÇDOĞAN
Alper ERDİNÇ
Mahmut BUT
Galip DİLER

## Special Thanks

-Assoc. Prof. Dr. Mustafa Berkan BİÇER for his Microprocessors Course
-Research Assistant A. Abbas ELMAS for his Microprocessors Lab. Course

 


