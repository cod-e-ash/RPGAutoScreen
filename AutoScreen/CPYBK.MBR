     ‚* Project     : AB Utilities (LIC:xxxxxx)                            *
     ‚* Programmer  : Ashish Bagaddeo                                      *
     ‚* Date        : 01/01/2014                                           *
     ‚* Description : Copybook                                             *
     ‚* × Copyright  : iCORE®            mailto: support@icore.co.in       *
     ‚**********************************************************************

     DCHANGEDCMD       S            512    INZ
     DCMDSTRING        S            512    INZ
     DCMDLENGTH        S             10I 0 INZ
     DCMDAVAILLEN      S             10I 0 INZ
     DCMDCHANGELEN     S             10I 0 INZ

     D APIERRORDS      DS                  INZ QUALIFIED
     D  BYTESPROV                    10I 0 INZ(%SIZE(APIERRORDS.MSGDATA))
     D  BYTESAVAL                    10I 0
     D  MSGID                         7A
     D  FILLER                        1A
     D  MSGDATA                     256A

     docbDS            ds                  Qualified
     d type                          10i 0 inz
     d DBCSdh                         1    inz('0')
     d prompt                         1    inz('0')
     d cmdsyntax                      1    inz('0')
     d msgrtvkey                      4    inz(x'00000000')
     d reserve1                       9    inz(x'000000000000000000')
     d ocblength                     10i 0 inz
     d formatName                     8    inz('CPOP0100')
     d chgcmd                         1    inz
     d lngchgcmd                     10i 0 inz
     d lngchgrtn                     10i 0 inz
     ‚* Prototypes
     D RunCmd          PR                  EXTPGM('QCMDEXC')
     D Command                      300
     D CommandLen                    15P 5

     D VALLSRCP        PR                  EXTPGM('VALLSRCP')
     D FileName                      10
     D FoundFlg                        N

     D CHKOUSGP        PR                  EXTPGM('CHKOUSGP')
     D ObjectName                    10
     D FoundFlg                        N

     D CHKFUSGP        PR                  EXTPGM('CHKFUSGP')
     D ObjectName                    10
     D FoundFlg                        N

     D VIEWFLDP        PR                  EXTPGM('VIEWFLDP')
     D ObjectName                    10
     D Library                       10
     D DisplayType                    1    Const
     D FoundFlg                        N

     D VIEWKEYP        PR                  EXTPGM('VIEWKEYP')
     D ObjectName                    10
     D Library                       10
     D FoundFlg                        N

     D VIEWMBRP        PR                  EXTPGM('VIEWMBRP')
     D ObjectName                    10
     D Library                       10
     D FoundFlg                        N

     D VIEWLGLP        PR                  EXTPGM('VIEWLGLP')
     D ObjectName                    10
     D Library                       10
     D FoundFlg                        N

     D FNDFLDP         PR                  EXTPGM('FNDFLDP')
     D FieldName                     10
     D FoundFlg                        N

     D VARCSRCP        PR                  EXTPGM('VARCSRCP')
     D ObjectName                    10
     D FoundFlg                        N

     D LIBLISTP        PR                  EXTPGM('LIBLISTP')
     D FoundFlg                        N

     D PRUNCMD         PR                  EXTPGM('QCAPCMD')
     D CMDSTRING                    512    CONST
     D CMDLENGTH                     10I 0 CONST
     D OCB                                 LIKEDS(OCBDS)
     D OCBLENGTH                     10I 0 CONST
     D FORMATNAME                     8    CONST
     D CHANGEDCMD                   512    CONST
     D LENAVAILCHGD                  10I 0 CONST
     D LENCHGDCMD                    10I 0 CONST
     D APIERROR                            LIKEDS(APIERRORDS)


     ‚*---------------------------------------------------------------------*
