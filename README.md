# CBT407
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 407 CONTAINS A COPY OF DYNAMIC BLDL FROM COMNET IN        *   FILE 407
//*           WASHINGTON D.C. AND WAS WRITTEN BY MR DAVID B COLE.   *   FILE 407
//*           THIS FILE IS IN IEBUPDTE SYSIN FORMAT (SEE THE        *   FILE 407
//*           MEMBER CALLED $$DOC FOR ADDITIONAL DOCUMENTATION).    *   FILE 407
//*                                                                 *   FILE 407
//*           Colesoft Marketing, Inc.                              *   FILE 407
//*           414 3rd ST. NE                                        *   FILE 407
//*           Charlottesville, VA 22902 USA                         *   FILE 407
//*           540-456-8210                                          *   FILE 407
//*           www.colesoft.com                                      *   FILE 407
//*           email:  dbcole@gmail.com                              *   FILE 407
//*                                                                 *   FILE 407
//*           THE MACROS NEEDED ARE CONTAINED IN FILE 408 OF        *   FILE 407
//*           THIS TAPE AND THE DYNABLDL LOAD MODULE FOR THIS       *   FILE 407
//*           LEVEL OF SOURCE RESIDES IN FILE 035 OF THIS TAPE.     *   FILE 407
//*                                                                 *   FILE 407
//*           THIS PROGRAM IS CONCEPTUALLY BASED ON THE VARIOUS     *   FILE 407
//*           DYNAMIC BLDL PROGRAMS AVAILABLE FROM THE "CBT         *   FILE 407
//*           UTILITIES" TAPE.  HOWEVER, THIS VERSION IS A          *   FILE 407
//*           COMPLETE REWRITE THAT INCORPORATES A SERIES OF        *   FILE 407
//*           IMPROVEMENTS:                                         *   FILE 407
//*                                                                 *   FILE 407
//*           THIS FILE ALSO CONTAINS AN XA VERSION OF DYNABLDL.    *   FILE 407
//*           SEE THE MEMBER CALLED $$XADOC FOR ADDITIONAL          *   FILE 407
//*           INFORMATION.  THE XA VERSION OF DYNABLDL WAS          *   FILE 407
//*           WRITTEN BY JOHN ANDERSON AND JEFF BROIDO AT           *   FILE 407
//*           WESTERN UNION/EDS IN MAHWAH, NEW JERSEY.              *   FILE 407
//*                                                                 *   FILE 407
//*                 - THIS VERSION OF DYNABLDL IS                   *   FILE 407
//*                   CAPABLE OF RECOGNIZING AND HOOKING            *   FILE 407
//*                   INTO ANY OF SEVERAL VERSIONS OF               *   FILE 407
//*                   IBM'S IGC018.  THE RECOGNITION CODE           *   FILE 407
//*                   IS TABLE DRIVEN, AND ADDITIONAL               *   FILE 407
//*                   RECOGNITION TABLES CAN BE FAIRLY              *   FILE 407
//*                   EASILY ADDED.                                 *   FILE 407
//*                                                                 *   FILE 407
//*                 - THE RECOGNITION TABLES ARE                    *   FILE 407
//*                   COMPREHENSIVE.  EACH TABLE CONSISTS           *   FILE 407
//*                   OF FOUR PARTS.  THE FIRST, LABELED            *   FILE 407
//*                   "ID#" (WHERE "#" REPRESENTS AN                *   FILE 407
//*                   ARBITRARY UNIQUE NUMERIC SUFFIX),             *   FILE 407
//*                   MUST MATCH AN IGC018'S                        *   FILE 407
//*                   IDENTIFICATION HEADER.  THIS IS               *   FILE 407
//*                   USED TO DISTINGUISH ONE IGC018                *   FILE 407
//*                   FROM ANOTHER.  THE SECOND AND THIRD           *   FILE 407
//*                   PARTS, LABELED "SRCHPO#" AND                  *   FILE 407
//*                   "DFOUND#", MUST MATCH THE TWO                 *   FILE 407
//*                   LOCATIONS IN IGC018 WHERE DYNABLDL            *   FILE 407
//*                   INSERTS ITS JUMPS TO ITS INTERCEPT            *   FILE 407
//*                   ROUTINES.  THE FOURTH PART CONSISTS           *   FILE 407
//*                   OF A LIST OF DESCRIPTORS OF ALL               *   FILE 407
//*                   IBM PRIVATE DATA FIELDS REFERENCED            *   FILE 407
//*                   BY THE INTERCEPT ROUTINES.  MOST              *   FILE 407
//*                   OF THE DESCRIPTORS ARE S-CONS                 *   FILE 407
//*                   GIVING THE BASE REGISTER BY WHICH             *   FILE 407
//*                   IGC018 REFERENCES A FIELD AND THE             *   FILE 407
//*                   DISPLACEMENT OF THAT FIELD INTO               *   FILE 407
//*                   THE IBM PRIVATE CONTROL BLOCK.  THE           *   FILE 407
//*                   DYNABLDL INITIALIZATION ROUTINE               *   FILE 407
//*                   USES THIS LIST TO DYNAMICALLY                 *   FILE 407
//*                   MODIFY ALL MACHINE INSTRUCTIONS IN            *   FILE 407
//*                   THE TWO INTERCEPT ROUTINES SO THAT            *   FILE 407
//*                   THEY CORRECTLY MATCH THE PARTICULAR           *   FILE 407
//*                   VERSION OF IGC018 BEING HOOKED                *   FILE 407
//*                   INTO.  NOTE, THE TWO IBM PRIVATE              *   FILE 407
//*                   CONTROL BLOCKS INVOLVED HERE ARE              *   FILE 407
//*                   THE "BLDL WORK AREA" AND BLDL'S               *   FILE 407
//*                   "SVRB EXTENDED SAVE AREA".                    *   FILE 407
//*                                                                 *   FILE 407
//*                 - ALL ROUTINES RELATED TO DYNABLDL              *   FILE 407
//*                   HAVE BEEN CONSOLIDATED INTO A                 *   FILE 407
//*                   SINGLE PROGRAM.  THIS RELIEVES THE            *   FILE 407
//*                   POTENTIAL FOR ERRORS ARISING FROM             *   FILE 407
//*                   PARTIAL MODIFICATIONS.                        *   FILE 407
//*                                                                 *   FILE 407
//*                 - THE DYNAMIC BLDL TABLE IS NOW                 *   FILE 407
//*                   MAINTAINED BY A STRAIGHTFORWARD               *   FILE 407
//*                   "LEAST RECENTLY USED" ALGORITHM.              *   FILE 407
//*                   THE PREVIOUSLY USED PERIODIC SORTS            *   FILE 407
//*                   AND PARTIAL REFILL METHOD HAS BEEN            *   FILE 407
//*                   DISCARDED.                                    *   FILE 407
//*                                                                 *   FILE 407
//*                 - PRIOR VERSIONS OF DYNABLDL DID                *   FILE 407
//*                   NOT INTERCEPT LINKLIST BLDL                   *   FILE 407
//*                   REQUESTS IN WHICH THE USER                    *   FILE 407
//*                   REQUESTED TWO OR MORE NAMES.                  *   FILE 407
//*                   FURTHER, PRIOR DYNABLDLS DID NOT              *   FILE 407
//*                   COUNT SUCH IGNORED REQUESTS AS                *   FILE 407
//*                   "MISSES".  CONSEQUENTLY, THE "HIT             *   FILE 407
//*                   RATE" REPORTED BACK WAS                       *   FILE 407
//*                   INCORRECT.  (IT WAS TOO HIGH).                *   FILE 407
//*                   THIS VERSION OF DYNABLDL DOES                 *   FILE 407
//*                   HANDLE MULTI-ENTRY BLDL REQUESTS,             *   FILE 407
//*                   AND MY EXPERIENCE HAS BEEN THAT               *   FILE 407
//*                   THE TRUE HIT RATE HAS RISEN FROM              *   FILE 407
//*                   ABOUT 80% TO BETTER THAN 95%.                 *   FILE 407
//*                                                                 *   FILE 407
//*                 - THE REPORT FUNCTION NOW PRODUCES              *   FILE 407
//*                   THREE LISTINGS OF THE DYNAMIC                 *   FILE 407
//*                   TABLE (PRINTED IN 3-COLUMN FORMAT             *   FILE 407
//*                   USING LESS THAN 79 CHARACTERS PER             *   FILE 407
//*                   LINE - SUITABLE FOR 3270 DISPLAY).            *   FILE 407
//*                   ONE LISTING IS SORTED BY NAME; A              *   FILE 407
//*                   SECOND IS SORTED BY HITS COUNT;               *   FILE 407
//*                   THE THIRD IS SORTED BY L.R.U.                 *   FILE 407
//*                   CHARACTERISTIC.                               *   FILE 407
//*                                                                 *   FILE 407
//*                 - THE DYNABLDL STOP FUNCTION NOW                *   FILE 407
//*                   COMPLETELY REMOVES DYNABLDL FROM              *   FILE 407
//*                   THE SYSTEM RATHER THAN JUST                   *   FILE 407
//*                   DISABLING THE HOOK ROUTINES.                  *   FILE 407
//*                                                                 *   FILE 407
//*                 - THERE IS AN UPDATE FROM SAM GOLOB             *   FILE 407
//*                 - SO IF YOU WISH, YOU CAN EXCLUDE UP            *   FILE 407
//*                 - TO SIX LINKLIST LIBRARIES FROM THE            *   FILE 407
//*                 - SEARCH.                                       *   FILE 407
//*                                                                 *   FILE 407
```
