# CBT172
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 172 is from David Cartwright of Lynn, Lichfield  in       *   FILE 172
//*           England.  This file contains a nice collection of     *   FILE 172
//*           utilities and useful tools.                           *   FILE 172
//*                                                                 *   FILE 172
//*           (UPDATED Dec 2012)                                    *   FILE 172
//*                                                                 *   FILE 172
//*           email:  dcartwright@ymail.com                         *   FILE 172
//*                                                                 *   FILE 172
//*      Neither David Cartwright nor any company associated        *   FILE 172
//*      with him express or imply any warranty as to the           *   FILE 172
//*      fitness of these computer programs for any function.       *   FILE 172
//*      The use of these programs or the results thereof is        *   FILE 172
//*      entirely at the risk of the user.                          *   FILE 172
//*                                                                 *   FILE 172
//*      These programs are donated to the public domain and may    *   FILE 172
//*      be freely copied. They may be freely distributed to any    *   FILE 172
//*      other party on condition that no inducement beyond         *   FILE 172
//*      reasonable handling costs be offered or accepted for       *   FILE 172
//*      such distribution.                                         *   FILE 172
//*                                                                 *   FILE 172
//*      These programs may be modified in any way the user         *   FILE 172
//*      thinks fit because use of these programs is entirely at    *   FILE 172
//*      the risk of the user anyway. I would be interested to      *   FILE 172
//*      hear of significant enhancements or instances where        *   FILE 172
//*      these programs have been of major benefit (or              *   FILE 172
//*      otherwise), but that depends purely on the politeness      *   FILE 172
//*      of the user.  Contact;                                     *   FILE 172
//*                                                                 *   FILE 172
//*               David Cartwright                                  *   FILE 172
//*               Lynn Farmhouse,                                   *   FILE 172
//*               Lynn Lane,                                        *   FILE 172
//*               Lynn,                                             *   FILE 172
//*               SHENSTONE, Staffordshire                          *   FILE 172
//*               UK - WS14 0EP                                     *   FILE 172
//*               tel.  ++44 (0)1543 481918                         *   FILE 172
//*                                                                 *   FILE 172
//*      A lot of these programs are out of date, being written     *   FILE 172
//*      for MVS/XA. However, with the interest in retro-computing  *   FILE 172
//*      created by the Hercules project I will not prune them out  *   FILE 172
//*      so that future generations can have a good laugh.          *   FILE 172
//*      (http://www.i-foo.com/hercules/)                           *   FILE 172
//*                                                                 *   FILE 172
//*      These goodies fall into different categories, as           *   FILE 172
//*      described below.  Assembly of many these programs          *   FILE 172
//*      requires SYS1.AMODGEN.  They have been tested on MVS/XA    *   FILE 172
//*      2.2, and some are known to work on other versions of       *   FILE 172
//*      MVS.  The programs written by me are reasonably well       *   FILE 172
//*      documented, but check that the code is doing what it       *   FILE 172
//*      says it is.  Programs like 'MAPDISK' which have been       *   FILE 172
//*      built up over the years should be viewed with              *   FILE 172
//*      suspicion, especially the preamble. All JCL should be      *   FILE 172
//*      viewed as being illustrative only, as a lot of junk        *   FILE 172
//*      tends to get left in as comments or unused ddnames.        *   FILE 172
//*      Always use the latest macros and copy code.                *   FILE 172
//*                                                                 *   FILE 172
//*      I use one of the standard systems for obtaining            *   FILE 172
//*      authorization but for security I will not divulge what     *   FILE 172
//*      it is. To give you some help I have begun to use a         *   FILE 172
//*      private macro 'GETAUTH' to invoke these functions. The     *   FILE 172
//*      version in this file will only generate an mnote to        *   FILE 172
//*      warn you that authorization is required, how you           *   FILE 172
//*      provide it is up to you.                                   *   FILE 172
//*                                                                 *   FILE 172
//*      Browse member @INDEX for an overview of the contents       *   FILE 172
//*      Here is some old documentation;                            *   FILE 172
//*                                                                 *   FILE 172
//*                      DISK MAPPING UTILITIES                     *   FILE 172
//*                                                                 *   FILE 172
//*      Includes yet another version of the ubiquitous             *   FILE 172
//*      'MAPDISK' that is indispensable for storage management.    *   FILE 172
//*      This version should be device independent and has some     *   FILE 172
//*      good features, such as dynamically allocating the VVDS     *   FILE 172
//*      on the volume and extracting information about VSAM        *   FILE 172
//*      files, e.g. tracks used. At last you can easily spot       *   FILE 172
//*      those hugely over-allocated VSAM hogs. also shows true     *   FILE 172
//*      last ref. date for VSAM without IDATMSTP (from VVDS)       *   FILE 172
//*      and will optionally write summary records for post         *   FILE 172
//*      processing. A cut-down version called 'MAPDLSIT' will      *   FILE 172
//*      read these summary records and create a MAPDISK style      *   FILE 172
//*      report.  Included is a sample job using this               *   FILE 172
//*      combination to report vastly over-allocated files and      *   FILE 172
//*      badly fragmented VSAM files (excessive splits). Now        *   FILE 172
//*      with SMS support.  MAPDISK programs have been updated      *   FILE 172
//*      August 2001                                                *   FILE 172
//*                                                                 *   FILE 172
//*      MAPDISK   Map disk contents with icf/VSAM details          *   FILE 172
//*      MAPDISKF  MAPDISK summary record format                    *   FILE 172
//*      MAPDLIST  Print MAPDISK summary records in MAPDISK format  *   FILE 172
//*      MAPDJCL   Sample JCL for MAPDISK programs                  *   FILE 172
//*      IXVTOCF5  Pseudo format 5 dscb's for indexed VTOCs         *   FILE 172
//*      VSMERROR  VSAM error routine from German G.U.I.D.E tape    *   FILE 172
//*      VVRDSECT  VVR record formats                               *   FILE 172
//*                                                                 *   FILE 172
//*      I developed a program to give an overview of 3380 status,  *   FILE 172
//*      which got developed for 3390's (not mod. 6).               *   FILE 172
//*      As a contractor I found the UCB scan routine changed       *   FILE 172
//*      with different releases of MVS, so I needed different      *   FILE 172
//*      versions of these programs.                                *   FILE 172
//*                                                                 *   FILE 172
//*      MAP3380   Overview of 3380's, by type (D,E,K). ESA V4      *   FILE 172
//*      MAP3390   OVerview of 3390's, by type (1,2,3). ESA V4      *   FILE 172
//*      M80ESA3   Overview of 3380's, by type (D,E,K). ESA V3      *   FILE 172
//*      M90ESA3   Overview of 3390's, by type (1,2,3). ESA V3      *   FILE 172
//*      M80XA2    Overview of 3380's, by type (D,E,K). MVS/XA V2   *   FILE 172
//*                                                                 *   FILE 172
//*                      VSAM HANDLING UTILITIES                    *   FILE 172
//*                                                                 *   FILE 172
//*      If you combine the VVDS processing I obtained from the     *   FILE 172
//*      German G.U.I.D.E. goodies tape for 'MAPDISK' with the      *   FILE 172
//*      SVC26 functions I got from the CBT tape (DSAT), you        *   FILE 172
//*      have some pretty powerful technology.  Give 'CAVEAT' a     *   FILE 172
//*      free-form list of VSAM items and it will generate          *   FILE 172
//*      ADCAMS ALTER cards to optimise buffer allocations.         *   FILE 172
//*      Unfortunately DFSMS no loger allows you to alter the       *   FILE 172
//*      BUFNI value, but 'CAVEAT' can still be used to set the     *   FILE 172
//*      total bufferspace.                                         *   FILE 172
//*                                                                 *   FILE 172
//*      AMDSB     Map AMDSBCAT area from SVC26                     *   FILE 172
//*      CATREAD   Use SVC26 to access ICF catalogs                 *   FILE 172
//*      CAVEAT    Cartwright's Amazing VSAM Entity Automatic       *   FILE 172
//*                Tuning                                           *   FILE 172
//*      EMPTOR    Disappointing, a sort of dis-IDCAMS, does        *   FILE 172
//*                AIX's                                            *   FILE 172
//*      GETVVR    Sub-program to return VVR data for an entity     *   FILE 172
//*      ICFDSECT  ICF catalog BCS data formats                     *   FILE 172
//*      JOBBUFNI  Sample daily update from SMF data                *   FILE 172
//*      RESULT    Data area returned from SVC26 program            *   FILE 172
//*                                                                 *   FILE 172
//*                   OUTPUT MANAGEMENT SYSTEM                      *   FILE 172
//*                                                                 *   FILE 172
//*      0nce upon a time (1982) I wrote a program which would      *   FILE 172
//*      act like an external writer and would store on tape the    *   FILE 172
//*      sysout which you did not want to print. I subsequently     *   FILE 172
//*      used commercial sysout managers including INFOPAC and      *   FILE 172
//*      SAR.  With the advent of System Managed Storage I          *   FILE 172
//*      thought my little external writer could be made just as    *   FILE 172
//*      good or better than those, so I did. This code will        *   FILE 172
//*      archive your sysout on disk where HSM can manage it. It    *   FILE 172
//*      is Cartwright's Housekeeping External Writer (CHEW). No    *   FILE 172
//*      bells, some whistles, but awfully cost effective.  Y2K     *   FILE 172
//*      compliant 1998                                             *   FILE 172
//*                                                                 *   FILE 172
//*      CHEW$DOC  Documentation                                    *   FILE 172
//*      CHEW$INST Assemble and link                                *   FILE 172
//*      CHEW$JCL  Run as a batch job                               *   FILE 172
//*      CHEWMAIN,CHEWDYNA,CHEWPARS,CHEWREPT   Source code          *   FILE 172
//*      CHEWSKIP,CHEWBACA,CHEWCOMM            Data areas           *   FILE 172
//*      CHEWOUT   is a separate program to print the last          *   FILE 172
//*                version of an archived report.                   *   FILE 172
//*                                                                 *   FILE 172
//*                  DATA COMPRESSION UTILITIES                     *   FILE 172
//*                                                                 *   FILE 172
//*      A set of programs to compress sequential files. I got      *   FILE 172
//*      fed up with waiting for operators to mount SMF tapes,      *   FILE 172
//*      so found a way to be able to keep SMF data online          *   FILE 172
//*      without consuming vast amounts of disk space.  'SSDC02'    *   FILE 172
//*      achieves about 40 percent space reduction by duplicate     *   FILE 172
//*      byte compression. In order to be able to manipulate        *   FILE 172
//*      compressed files directly I use the facilities of          *   FILE 172
//*      DF/SORT via E15 exits. In response to the poor results     *   FILE 172
//*      achieved by 'SSDC02' when shrinking user files that had    *   FILE 172
//*      few repeating characters, I wrote a program calling the    *   FILE 172
//*      Huffman tree compaction routine from 'ARCHIVER', by        *   FILE 172
//*      Richard A. Fochtman (CBT file 147). On SMF data this       *   FILE 172
//*      program gives output about 10 percent smaller than         *   FILE 172
//*      'SSDC02'. However, to expand the data takes three times    *   FILE 172
//*      as much CPU time as using 'SSDCE15'.  I later wrote        *   FILE 172
//*      DCPCOMP1 to improve on SSDC02 and then DCPCOMP2 for SMF    *   FILE 172
//*      data - the results of this are spectacular if you sort     *   FILE 172
//*      on the SMF header first. DCS....  members are SORT exit    *   FILE 172
//*      versions of these programs.                                *   FILE 172
//*                                                                 *   FILE 172
//*      ACTOR     ARCHIVER Compaction Technique Output Reduction   *   FILE 172
//*      ACTRESS   ARCHIVER Compaction Rechnique Rebuild Exit       *   FILE 172
//*                for SortS                                        *   FILE 172
//*      COMPACT   Object deck for ARCHIVER compaction code (RENT)  *   FILE 172
//*      EXPAND    Object deck for ARCHIVER expansion code (RENT)   *   FILE 172
//*      SSDC02    Data utility 1 - compress data                   *   FILE 172
//*      SSDC03    Data utility 2 - expand data                     *   FILE 172
//*      DCPCOMP1  Compression program with improved algorithm      *   FILE 172
//*      DCPCOMP2  Compression program for SMF data                 *   FILE 172
//*      DCPEXPD1  Expand program for improved algorithm            *   FILE 172
//*      DCPEXPD2  Expand program for SMF data                      *   FILE 172
//*      SSDCE15   Data utility 2 - expand data sort exit E15       *   FILE 172
//*                                                                 *   FILE 172
//*              SMF/RMF DATA MANIPULATION UTILITIES                *   FILE 172
//*                                                                 *   FILE 172
//*      Various programs to make it easier to handle SMF           *   FILE 172
//*      records for performance reporting, particularly using      *   FILE 172
//*      simple report writers such as CA/EARL. See also the        *   FILE 172
//*      programs adapted from other CBT offerings.                 *   FILE 172
//*                                                                 *   FILE 172
//*      CRAP      Cartwright's Racf Accounting Program             *   FILE 172
//*      CUSS23    User2 exit for IFASMFDP to delete SMF2 and 3     *   FILE 172
//*      DAVE73    RMF channel records                              *   FILE 172
//*      DAVE73PR  Report on channel utilisation                    *   FILE 172
//*      DAVE74    RMF device records                               *   FILE 172
//*      SEAFOOD   Re-format SMF date to include month              *   FILE 172
//*      SENDOFF   User exit for IFASMFDP to only select workdays   *   FILE 172
//*      SERVED70  Create summary records from SMF70 data           *   FILE 172
//*      SERVED71  Create summary records from SMF71 data           *   FILE 172
//*      SERVED72  Create summary records from SMF72 data           *   FILE 172
//*      SE70REC   RMF 70 summary record format from 'SERVED70'     *   FILE 172
//*      SE71REC   RMF 71 summary record format from 'SERVED71'     *   FILE 172
//*      SE72REC   RMF 72 summary record format from 'SERVED72'     *   FILE 172
//*      SE80REC   SMF 80 summary record format from 'CRAP'         *   FILE 172
//*      STROBE    Visual display of multiprogramming (PL/1)        *   FILE 172
//*                                                                 *   FILE 172
//*               OTHER DATA MANIPULATION UTILITIES                 *   FILE 172
//*                                                                 *   FILE 172
//*      Various programs to do odd things.                         *   FILE 172
//*                                                                 *   FILE 172
//*      ASTRA     Find named task - used in TSSO automation.       *   FILE 172
//*      FSF       To automate FLEX-ES "FakeTape"(tm) reads TMC.    *   FILE 172
//*      DCFON     ISPF edit macro to convert from UOW SCRIPT to    *   FILE 172
//*                DCF/GML                                          *   FILE 172
//*      DAYOWEEK  Set return code by day of week                   *   FILE 172
//*      DAYOMNTH  Set return code by day of month                  *   FILE 172
//*      DEVOFF    Vary device offline under control of opc/a       *   FILE 172
//*      EMPTYPDS  Reset PDS directory and high water mark          *   FILE 172
//*      HPR       HSM Problem Reporter -                           *   FILE 172
//*                print explanation of HSM SMF records             *   FILE 172
//*      ICF3490   Catalog conversion program for 3480 to 3490      *   FILE 172
//*      LOGAN     IBM SYSLOG analysis program from GG24-3142-01    *   FILE 172
//*      RLSEJCL   JCL for using 'VTOC' in batch to release space   *   FILE 172
//*      SETOFF    Calls OPC/A Event Writer interface               *   FILE 172
//*      SSWAIT    Program to wait, may be stopped by 'P' command   *   FILE 172
//*      S36PRTU4  Print SYSTEM/36 output under MVS                 *   FILE 172
//*                                                                 *   FILE 172
//*                  MVS MESSAGE PROCESSING MODS                    *   FILE 172
//*                                                                 *   FILE 172
//*      Although I use 'TSSO' for most console automation,         *   FILE 172
//*      there are occasions when a straight MPF exit is the        *   FILE 172
//*      best way to do it.  here are some examples.                *   FILE 172
//*                                                                 *   FILE 172
//*      IEAVMXIT  Default MPF exit - label and suppress WTO        *   FILE 172
//*      MPFTAPEM  MPF exit to SMF record tape mount, find volume   *   FILE 172
//*      MPFTAPEK  Taintain tape tables in CSA                      *   FILE 172
//*      MPFTAPET  Copy block to initialise unit volume tables      *   FILE 172
//*      MPFTAPEQ  Program to enquire on tape mount tables (for     *   FILE 172
//*                TSSO)                                            *   FILE 172
//*      GETUCVTR  Re-entrant routine to find or build the user     *   FILE 172
//*                CVT                                              *   FILE 172
//*      USERCVT   Format of user CVT hung out of 'CVTUSER' field   *   FILE 172
//*      CSATABLE  Format of in storage tape volser table           *   FILE 172
//*      SMF234    Format of SMF record for tape unit activity      *   FILE 172
//*                                                                 *   FILE 172
//*                 MISCELLANEOUS MVS MODIFICATIONS                 *   FILE 172
//*                                                                 *   FILE 172
//*      Here are some assorted mods for IBM program products.      *   FILE 172
//*      Some of them are available from various samplibs, but      *   FILE 172
//*      they are offered here to act as templates for your own     *   FILE 172
//*      tailoring. The sort mods are designed to stop DF/SORT      *   FILE 172
//*      fixing pages during prime shift. The sort defaults are     *   FILE 172
//*      altered to call the input exit which determines whether    *   FILE 172
//*      to use EXCPVR. Very out of date now                        *   FILE 172
//*                                                                 *   FILE 172
//*      DRKUX006  assembly of OPC/A incident record create exit    *   FILE 172
//*      SMIXRECE  Install DF/SORT input exit ICEIEXIT              *   FILE 172
//*      SMIXAPPE  Apply DF/SORT input exit usermod (do not         *   FILE 172
//*                accept)                                          *   FILE 172
//*      SMOPRECE  Receive usermod to alter DF/SORT defaults        *   FILE 172
//*      SMOPAPPE  Apply usermod to alter DF/SORT defaults          *   FILE 172
//*      LASSOO    Set an address space swappable/nonswappable      *   FILE 172
//*      DEMAND    Delete members of PDS 'A' from PDS 'B'           *   FILE 172
//*                                                                 *   FILE 172
//*                    SIEMENS/STC LASER PRINTER GOODIES            *   FILE 172
//*                                                                 *   FILE 172
//*      Various fonts etc. for a 3800-3 type printer running       *   FILE 172
//*      in 3800-1 compatability mode. For the real IBM box you     *   FILE 172
//*      will have to change the device specified and use           *   FILE 172
//*      'IEBIMAGE' instead of the Siemens version. A lot of        *   FILE 172
//*      this stuff is about Swiss National Language Support        *   FILE 172
//*      which is based on Code Page 500, so may be of interest     *   FILE 172
//*      to international companies. If you use exclusively         *   FILE 172
//*      U.S.  English (now there's an oxymoron) you may skim       *   FILE 172
//*      through for examples of IEBIMAGE or something like it,     *   FILE 172
//*      and of course the fonts are still valid.                   *   FILE 172
//*                                                                 *   FILE 172
//*      chars19v  Swiss NLS version of font 019v, 15 pitch         *   FILE 172
//*                Gothic.                                          *   FILE 172
//*      S9A1      Gothic rotated swiss (GROSS) version of font     *   FILE 172
//*                017V                                             *   FILE 172
//*      LN12      12 lpi FCB for rotated listings                  *   FILE 172
//*      SE526     translate in-place upper/lower case (Swiss)      *   FILE 172
//*                and ASCII                                        *   FILE 172
//*      WCGMLST1  Documentation on standard WCGM assignments       *   FILE 172
//*      WCGMLST2  Documentation on our (NLS) WCGM assignments      *   FILE 172
//*                                                                 *   FILE 172
//*                   CACHE MANAGEMENT PROGRAMS                     *   FILE 172
//*                                                                 *   FILE 172
//*      These programs are for MVS installations using the IBM     *   FILE 172
//*      3990-3 disk controller with cache. I include a simple      *   FILE 172
//*      cache performance monitor program. The other programs      *   FILE 172
//*      are intended to modify various modules in storage to       *   FILE 172
//*      allow the paging and/or swapping sub-system to use the     *   FILE 172
//*      3990-3 extended functions Cache Fast Write (CFW) or        *   FILE 172
//*      DASD Fast Write (DFW).  The member '$PAPER' will give      *   FILE 172
//*      the user some idea of the purpose, benefits and            *   FILE 172
//*      problems of the programs supplied.  Updated October        *   FILE 172
//*      1992                                                       *   FILE 172
//*                                                                 *   FILE 172
//*      $PAPER    Text giving history of cache developments (asa)  *   FILE 172
//*      SECR01    Cache reporting program                          *   FILE 172
//*      SECOMMON  Cuxiliary storage manager zap common code        *   FILE 172
//*      SECFWON   Cllow paging to use cache fast write             *   FILE 172
//*      SECFWOFF  Zap storage back to IBM values                   *   FILE 172
//*      SECFWMPF  MPF exit to disable cache fast write             *   FILE 172
//*      SEDFWON   Allow paging to use dasd fast write              *   FILE 172
//*      SEDFWOFF  Turn off dasd fast write for paging              *   FILE 172
//*      SEREC     IBM 3990-3 subsystem statistics record           *   FILE 172
//*      SESMF     Cache monitor SMF record                         *   FILE 172
//*                                                                 *   FILE 172
//*                   MODIFIED PUBLIC DOMAIN PROGRAMS               *   FILE 172
//*                                                                 *   FILE 172
//*      Here are some programs which have been slightly modified   *   FILE 172
//*      for local conditions. Most of them came from the CBT       *   FILE 172
//*      tape at various times.  My thanks to the original          *   FILE 172
//*      authors.                                                   *   FILE 172
//*                                                                 *   FILE 172
//*      CCKDDUMP  Greg Smith's DASD dumper for Hercules            *   FILE 172
//*      CCKDLOAD  Greg Smith's DASD loader for Hercules            *   FILE 172
//*      CPUID     Changes the CPUID in PCCAs                       *   FILE 172
//*                for disaster recovery purposes, at the           *   FILE 172
//*                disaster recovery site.                          *   FILE 172
//*      EDX       Jim Lane's clist ex File047 with multiple        *   FILE 172
//*                lists                                            *   FILE 172
//*      FILE171   Fixes to FILE171 - DITTO                         *   FILE 172
//*      GETDATE   USAF program to do date conversion + holiday     *   FILE 172
//*                table                                            *   FILE 172
//*      LISTPDS   New version (8.4), can punch ./ ALIAS cards      *   FILE 172
//*                and upgraded for new ISPF stats and 8-character  *   FILE 172
//*                userids (see comments in the code)               *   FILE 172
//*      LISTPDSO  Unnumbers members when unloading                 *   FILE 172
//*      LISTICF  Lline per entry catalog lister                    *   FILE 172
//*      ROTATES   My version of U.S.A.F. page rotate program.      *   FILE 172
//*      SE30EXT   A special version of SUM30EXT including RACF     *   FILE 172
//*                fields                                           *   FILE 172
//*      SE30RPT   SEAG version of SMF30 summary - larger time      *   FILE 172
//*                fields                                           *   FILE 172
//*      SE30REC   SEAG version of SMF30 summary records            *   FILE 172
//*      SMF1415   Report on non-VSAM file activity                 *   FILE 172
//*      SPMGCLD   Front end for IDCAMS uses esoteric names         *   FILE 172
//*      STRING    Macro for MPFTAPE. exits - build unit tables     *   FILE 172
//*      STRNGEND  Macro for MPFTAPE. exits - build unit tables     *   FILE 172
//*      SYSEVENT  SYSEVENT analysis system from Standard Oil       *   FILE 172
//*      SYSIEH    IEHPROGM without enqueues                        *   FILE 172
//*      TRUISMS   A few thoughts for 'MURPHY'                      *   FILE 172
//*                                                                 *   FILE 172
//*      In this category I include my enhancements for version     *   FILE 172
//*      5 of 'The ARCHIVER' from CBT file 147. These are           *   FILE 172
//*      designed to perform an automatic alias and delete          *   FILE 172
//*      function after running a compare.                          *   FILE 172
//*                                                                 *   FILE 172
//*      ARCHCOMP  ARCHIVER compare program including my inserts    *   FILE 172
//*      ARCHPARS  ARCHIVER parsing program including my inserts    *   FILE 172
//*      CRAMP     Generate delete and alias cards                  *   FILE 172
//*      CRAMPON   Invoke my autoarchive program                    *   FILE 172
//*      CRAMPOFF  Delete my autoarchive program                    *   FILE 172
//*                                                                 *   FILE 172
//*                      MACROS AND COMMON CODE                     *   FILE 172
//*                                                                 *   FILE 172
//*      As well as text and program source there are some          *   FILE 172
//*      members which are copied into the programs and some        *   FILE 172
//*      macros. Most of those are from the Public Domain i.e. I    *   FILE 172
//*      gave them away before I quit.                              *   FILE 172
//*                                                                 *   FILE 172
//*      Around the end of 1991 I started to write a lot more       *   FILE 172
//*      re-usable code by splitting small functional               *   FILE 172
//*      sub-routines out into copy blocks. These are also          *   FILE 172
//*      included in this file.                                     *   FILE 172
//*                                                                 *   FILE 172
//*                            *** end ***                          *   FILE 172
//*                                                                 *   FILE 172
```
