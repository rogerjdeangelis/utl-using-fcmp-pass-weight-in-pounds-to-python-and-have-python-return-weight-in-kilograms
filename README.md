# utl-using-fcmp-pass-weight-in-pounds-to-python-and-have-python-return-weight-in-kilograms
Using fcmp pass weight in pounds to python and have python return weight in kilograms
    %let pgm=utl-using-fcmp-pass-weight-in-pounds-to-python-and-have-python-return-weight-in-kilograms;

    %stop_submission;

    Using fcmp pass weight in pounds to python and have python return weight in kilograms

    PROBLEM: Convert lbs to kg

        CONTENTS

           1 fcmp & sas mas2py.py
             NOTE: I copied the file below to d:/py/mas2py.py
             C:\Program Files\SASHome\SASFoundation\9.4\tkmas\sasmisc\mas2py.py
             Bartosz Jablonski
             yabwon@gmail.com

           2 save d:/py/mas2py.py
             NOTE: I copied the file below to d:/py/mas2py.py
             C:\Program Files\SASHome\SASFoundation\9.4\tkmas\sasmisc\mas2py.py

    github
    https://tinyurl.com/4dcu73dy
    https://github.com/rogerjdeangelis/utl-using-fcmp-pass-weight-in-pounds-to-python-and-have-python-return-weight-in-kilograms

    communities.sas
    https://tinyurl.com/6f5w5aj4
    https://communities.sas.com/t5/SAS-Programming/proc-fcmp-python-code-shows-no-output-on-submission/m-p/773931#M245922

    /**************************************************************************************************************************/
    /*       INPUT                 |           PROCESS                             |     OUTPUT                               */
    /*       =====                 |           =======                             |     ======                               */
    /* WORK.HAVE OBS=3             | 1 FCMP & SAS MAS2PY.PY                        | WORK.WANT total obs=3        COMPUTED    */
    /*                             | ======================                        |                              BY PYTHON   */
    /*  NAME      AGE    WGTLBS    |                                               |   NAME      AGE    WGTLBS     WGTKGS     */
    /*                             | You need to do these two steps first          |                                          */
    /* Alfred      14     112.5    |                                               |  Alfred      14     112.5    51.1364     */
    /* Alice       13      84.0    | 1. You need to run the code in step 2 above   |  Alice       13      84.0    38.1818     */
    /* Barbara     13      98.0    |    2 COPY MAS2PY.PY TO C:/PY/MAS2PY.PY        |  Barbara     13      98.0    44.5455     */
    /*                             |    or use full path in fcmp below             |                                          */
    /*                             |                                               |                                          */
    /* data have;                  | 2  python.exe needs to be in your path or     |                                          */
    /*   set sashelp.class         |    supply full path in fcmp program           |                                          */
    /*      (obs=3                 |                                               |                                          */
    /*       keep=                 |                                               |                                          */
    /*         name                | options                                       |                                          */
    /*         age                 |   set=MAS_PYPATH="python.exe"                 |                                          */
    /*         weight              |   set=MAS_M2PATH "d:\py\mas2py.py"            |                                          */
    /*      rename=weight=wgtlbs); |   cmplib=work.fcmp;                           |                                          */
    /* run;quit;                   |                                               |                                          */
    /*                             | proc fcmp outlib=work.fcmp.pyfuncs;           |                                          */
    /*                             |                                               |                                          */
    /*                             | function lb2kg(SASArg);                       |                                          */
    /*                             | declare object py(python('MySASFunc'));       |                                          */
    /*                             | submit into py;                               |                                          */
    /*                             | def MyFunc(arg1):                             |                                          */
    /*                             |    "Output: MyKey"                            |                                          */
    /*                             |    ReturnVar = arg1/2.2                       |                                          */
    /*                             |    return ReturnVar                           |                                          */
    /*                             | endsubmit;                                    |                                          */
    /*                             | rc = py.publish();                            |                                          */
    /*                             | rc = py.call("MyFunc", SASArg);               |                                          */
    /*                             | x = py.results["MyKey"];                      |                                          */
    /*                             | return(x);                                    |                                          */
    /*                             |                                               |                                          */
    /*                             | endsub;                                       |                                          */
    /*                             | run;quit;                                     |                                          */
    /*                             |                                               |                                          */
    /*                             | data want;                                    |                                          */
    /*                             |   set work.have;                              |                                          */
    /*                             |   wgtkgs=lb2kg(wgtlbs);                       |                                          */
    /*                             | run;                                          |                                          */
    /*                             |                                               |                                          */
    /*                             |                                               |                                          */
    /*                             | 2 COPY MAS2PY.PY TO C:/PY/MAS2PY.PY           |                                          */
    /*                             | ===================================           |                                          */
    /*                             | see below                                     |                                          */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data have;
      set sashelp.class
         (obs=3
          keep=
            name
            age
            weight
         rename=weight=wgtlbs);
    run;quit;

    /**************************************************************************************************************************/
    /*       INPUT                                                                                                            */
    /*       =====                                                                                                            */
    /* WORK.HAVE OBS=3                                                                                                        */
    /*                                                                                                                        */
    /*  NAME      AGE    WGTLBS                                                                                               */
    /*                                                                                                                        */
    /* Alfred      14     112.5                                                                                               */
    /* Alice       13      84.0                                                                                               */
    /* Barbara     13      98.0                                                                                               */
    /**************************************************************************************************************************/

    /*    __                         ___                         ____
    / |  / _| ___ _ __ ___  _ __    ( _ )    _ __ ___   __ _ ___|___ \ _ __  _   _   _ __  _   _
    | | | |_ / __| `_ ` _ \| `_ \   / _ \/\ | `_ ` _ \ / _` / __| __) | `_ \| | | | | `_ \| | | |
    | | |  _| (__| | | | | | |_) | | (_>  < | | | | | | (_| \__ \/ __/| |_) | |_| |_| |_) | |_| |
    |_| |_|  \___|_| |_| |_| .__/   \___/\/ |_| |_| |_|\__,_|___/_____| .__/ \__, (_) .__/ \__, |
                           |_|                                        |_|    |___/  |_|    |___/
    You need to do these two steps first

    1. You need to run the code in step 2 above
       2 COPY MAS2PY.PY TO C:/PY/MAS2PY.PY
       or use full path in fcmp below

    2  python.exe needs to be in your path or
       supply full path in fcmp program
    */

    options
      set=MAS_PYPATH="python.exe"
      set=MAS_M2PATH "d:\py\mas2py.py"
      cmplib=work.fcmp;

    proc fcmp outlib=work.fcmp.pyfuncs;

    function lb2kg(SASArg);
    declare object py(python('MySASFunc'));
    submit into py;
    def MyFunc(arg1):
       "Output: MyKey"
       ReturnVar = arg1/2.2
       return ReturnVar
    endsubmit;
    rc = py.publish();
    rc = py.call("MyFunc", SASArg);
    x = py.results["MyKey"];
    return(x);

    endsub;
    run;quit;

    data want;
      set work.have;
      wgtkgs=lb2kg(wgtlbs);
    run;

    /**************************************************************************************************************************/
    /* WORK.WANT total obs=3       COMPUTED BY                                                                                */
    /*                              PYTHON                                                                                    */
    /*   NAME      AGE    WGTLBS     WGTKGS                                                                                   */
    /*                                                                                                                        */
    /*  Alfred      14     112.5    51.1364                                                                                   */
    /*  Alice       13      84.0    38.1818                                                                                   */
    /*  Barbara     13      98.0    44.5455                                                                                   */
    /**************************************************************************************************************************/

    /*___                             _      __              __                   ____
    |___ \   ___  __ ___   _____   __| |_   / / __  _   _   / / __ ___   __ _ ___|___ \ _ __  _   _   _ __   _   _
      __) | / __|/ _` \ \ / / _ \ / _` (_) / / `_ \| | | | / / `_ ` _ \ / _` / __| __) | `_ \| | | | | `_ \ | | | |
     / __/  \__ \ (_| |\ V /  __/| (_| |_ / /| |_) | |_| |/ /| | | | | | (_| \__ \/ __/| |_) | |_| |_| |_) || |_| |
    |_____| |___/\__,_| \_/ \___| \__,_(_)_/ | .__/ \__, /_/ |_| |_| |_|\__,_|___/_____| .__/ \__, (_) .__/  \__, |
                                             |_|    |___/                              |_|    |___/  |_|     |___/
    */

    filename ft15f001 "d:/py/mas2py.py";
    parmcards4;
    # (c) 2018, SAS Institute Inc.
    #-------------------------------------------------------------------------
    MAS2PY_VERSION = "2.1.0"


    ##########################################################################
    # Environment Variables
    #
    #   MAS_PYLOG_FILE:
    #       Will create a local Python Logging file.
    #       Default:  Filename is overwritten before logging.
    #       '+log.txt': will append data to 'log.txt'.
    #
    #   MAS_PYLOG_LEVEL:
    #       The logging level: { ALL, TRACE, DEBUG, INFO, WARN, ERROR, FATAL, OFF }
    #       Default: WARN
    #
    #   MAS_PYOUT_FILE:
    #       Filename for python process STDOUT / STDERR
    #       Default:  Filename is overwritten before logging.
    #       '+out.txt': will append data to 'out.txt'.
    #
    ##########################################################################


    try:
       import pandas as pd
    except:
       pd = None
    import sys
    import os
    import socket as socks
    import struct
    import tempfile
    from datetime import datetime, date, time, timedelta
    import calendar
    import traceback
    import operator as op
    import inspect as insp
    import shutil
    import codecs
    import platform
    from time import sleep
    import types
    import logging
    import math


    #  TODO:  Create Invoke class that captures invoke parameters for better error message at the Unpack/Pack level
    #
    #
    #
    #



    # Globals
    #-------------------------------------------------------------------------
    masTmpPath = ''
    MAS_MIN_REQ_MAJOR = 10
    MAS_MIN_REQ_MINOR = 0

    MASCmd_Publish = 0x01
    MASCmd_PublishFile = 0x02
    MASCmd_Invoke =  0x05
    MASCmd_Version = 0xc0
    MASCmd_Logging = 0xc1
    MASCmd_Complete = 0xcf
    MASCmd_Exception = 0xe0
    MASCmd_Shutdown = 0xf0

    # Exceptions
    #-------------------------------------------------------------------------
    class masException(Exception):
        pass


    # utility functions
    #-------------------------------------------------------------------------
    def getEnv(key,default=None):
        try:
            val = os.environ[key]
            if ((val.startswith('"') and val.endswith('"')) or (val.startswith("'") and val.endswith("'"))):
                val = val[1:-1]
        except:
            val = default
        return val

    def str2b(s):
      sval = str(s)
      return sval.lower() in ('yes','y','true','t','1')


    ##########################################################################
    # Logging
    #-------------------------------------------------------------------------

    # MasLog
    #-------------------------------------------------------------------------
    class MasLog:
       ALL    = 1
       TRACE  = 2
       DEBUG  = 3
       INFO   = 4
       WARN   = 5
       ERROR  = 6
       FATAL  = 7
       OFF    = 8
       lvlStr = { ALL:'ALL', TRACE:'TRACE', DEBUG:'DEBUG', INFO:'INFO', WARN:'WARN', ERROR:'ERROR', FATAL:'FATAL', OFF:'OFF' }
       lvlInt = { 'ALL':ALL, 'TRACE':TRACE, 'DEBUG':DEBUG, 'INFO':INFO, 'WARN':WARN, 'ERROR':ERROR, 'FATAL':FATAL, 'OFF':OFF }

       def __init(self,level):
           self._mas = None
           self._logLevel = level
           self._logFile = None
           try:
               logFilename = getEnv('MAS_PYLOG_FILE')
               if (logFilename):
                   if (logFilename[0] == '+'):
                       fmode = 'a'
                       logFilename = logFilename[1:]
                   else:
                       fmode = 'w'
                   self._logFile = open(logFilename, fmode)
           except:
               self._logFile = None
       def __init__(self, level):
           self.__init(level)
       def __init__(self):
           lvlName = getEnv('MAS_PYLOG_LEVEL','WARN')
           lvl = self.levelInt(lvlName)
           if (lvl is None):
               lvl = self.WARN
           self.__init(lvl)

       def levelStr(self, iLevel):
           try:
               val = self.lvlStr[iLevel]
           except:
               val = None
           return val
       def levelInt(self, sLevel):
           try:
               uc = sLevel.upper()
               val = self.lvlInt[uc]
           except:
               val = None
           return val

       def log(self, level, msg, *args, **kwargs):
           mas = True
           log = True
           for key, val in kwargs.items():
               key = key.lower()
               if (key == 'mas'):
                   mas = str2b(val)
               elif (key == 'log'):
                   log = str2b(val)
           msgS = str(msg)
           if (log and self._logFile):
               now = datetime.now()
               n = now.strftime('%Y-%m-%d %H:%M:%S') + '.' + str(now.microsecond)
               strLevel = self.levelStr(level)
               self._logFile.write("    " + n + " " + str(strLevel) + " " + msgS + "\n")
               self._logFile.flush()
           if (mas and self._mas):
               retPack = self._mas.packReturnMsg(MASCmd_Logging, msgS, level)
               self._mas.write(retPack)

       def all(self, msg, *args, **kwargs):
           ml = self.ALL
           self.log(ml, msg, *args, **kwargs)

       def trace(self, msg, *args, **kwargs):
           ml = self.TRACE
           ll = self._logLevel
           if ((ll == self.ALL) or (ml >= ll)):
               self.log(ml, msg, *args, **kwargs)

       def debug(self, msg, *args, **kwargs):
           ml = self.DEBUG
           ll = self._logLevel
           if ((ll == self.ALL) or (ml >= ll)):
               self.log(ml, msg, *args, **kwargs)

       def info(self, msg, *args, **kwargs):
           ml = self.INFO
           ll = self._logLevel
           if ((ll == self.ALL) or (ml >= ll)):
               self.log(ml, msg, *args, **kwargs)

       def warn(self, msg, *args, **kwargs):
           ml = self.WARN
           ll = self._logLevel
           if ((ll == self.ALL) or (ml >= ll)):
               self.log(ml, msg, *args, **kwargs)

       def error(self, msg, *args, **kwargs):
           ml = self.ERROR
           ll = self._logLevel
           if ((ll == self.ALL) or (ml >= ll)):
               self.log(ml, msg, *args, **kwargs)

       def fatal(self, msg, *args, **kwargs):
           ml = self.FATAL
           ll = self._logLevel
           if ((ll == self.ALL) or (ml >= ll)):
               self.log(ml, msg, *args, **kwargs)
    ##########################################################################




    ##########################################################################
    # C-Interface ABI
    #  TODO:  Why are we using integer instead of same CHAR as input?
    #  TODO:  Standardize on Input/Output type marshalling
    BOOLOID = 100
    INT8OID = 105
    FLOAT8OID = 106
    VARCHAROID = 108
    DATEOID = 111
    TIMEOID = 112
    C_DATEOID = 150
    null = b'\x00'
    ##########################################################################


    # python 3.3+ requires this for generated code files
    try:
        from importlib import invalidate_caches
    except:
        pass

    try:
        from importlib import reload # 3.4 and above
    except:
        try:
            from imp import reload # 2.x and <= 3.3
        except:
            pass # reload is built in for < 2.x

    try:
        if type('abc') == unicode:
            pass
    except:
        unicode = str

    try:
        long
    except:
        long = int





    ##########################################################################
    ## MAS2py Class
    ##########################################################################
    class MAS2py:
        """
        This is the main object for the mas2py python interface
        """

        # __init__
        #---------------------------------------------------------------------
        def __init__(self, **kwargs):
            self._masLog = MasLog()
            self._masLog.debug('MAS2py.__init__()')
            self.mode      = ''
            self._pyver    = 100
            self._seqID    = 0
            self._socket   = None

            #self.mascfg   = MASconfig(**kwargs)
            self.ups       = {}
            self.uf        = None
            self.insig     = None


        # read - read data
        #---------------------------------------------------------------------
        def read(self, n):
            data = b''
            while (n > 0):
                packet = self._socket.recv(n)
                if (not packet):
                    break
                data += packet
                n -= len(packet)
                if (n > 0):
                    sleep(0.01)
            return data


        # write - write the data
        #---------------------------------------------------------------------
        def write(self, buff):
            self._socket.sendall(buff)


        # connect - Connect to the MAS server
        #---------------------------------------------------------------------
        def connect(self, host, port, auth):
            # Socket connect
            self._masLog.debug('MAS2py.connect()')
            self._socket = socks.socket(socks.AF_INET, socks.SOCK_STREAM)
            self._socket.connect((host, port))
            self._socket.setsockopt(socks.SOL_TCP, socks.TCP_NODELAY, 1)
            self._masLog.debug('Socket Connected')

            # Send authentication
            self.write(auth)
            self._masLog.debug('Socket Authenticated')

            # Version Handshake
            self._masLog.debug('Version -Read')
            b = self.read(24)
            self._masLog.debug('Version Read')
            (self._tkMajor, self._tkMinor, self._tkDelta, self._masMajor, self._masMinor, self._masDelta) = struct.unpack('6i', b)
            self._masLog.debug('Version Received')
            self._masLog.debug('Version:  TK:  '+str(self._tkMajor)+'.'+str(self._tkMinor)+'.'+str(self._tkDelta))
            self._masLog.debug('Version:  MAS: '+str(self._masMajor)+'.'+str(self._masMinor)+'.'+str(self._masDelta))
            if ((self._masMajor < MAS_MIN_REQ_MAJOR) or
                ((self._masMajor == MAS_MIN_REQ_MAJOR) and (self._masMinor < MAS_MIN_REQ_MINOR))):
                msg = '  *****  Invalid MAS Version:  Required Minimum: '+str(MAS_MIN_REQ_MAJOR)+'.'+str(MAS_MIN_REQ_MINOR)+'x'
                self._masLog.error(msg)
                b = struct.pack('3i', 0, 0, 0)
                self.write(b)
                raise masException(msg)

            pyVer = platform.python_version_tuple()
            try:
                self._pyMajor  = int(pyVer[0].rstrip('+'))
                self._pyMinor  = int(pyVer[1].rstrip('+'))
                self._pyDelta  = int(pyVer[2].rstrip('+'))
            except:
                self._pyMajor  = 0
                self._pyMinor  = 0
                self._pyDelta  = 0
            self._masLog.debug('Version:  PYTHON: '+str(self._pyMajor)+'.'+str(self._pyMinor)+'.'+str(self._pyDelta))
            b = struct.pack('3i', self._pyMajor, self._pyMinor, self._pyDelta)
            self.write(b)
            self._masLog._mas = self
            self._masLog.debug('connect(): Finished')
            return


        # Generate Return message
        #---------------------------------------------------------------------
        def packReturnMsg(self, cmd, msg=None, level=None):
            seqID = self._seqID
            i = (((cmd & 0xff) << 24) | (seqID & 0xffffff))
            b = struct.pack('I', i)
            bSz = 0
            if (level != None):
                bSz += 8
            if (msg != None):
                if (type(msg) is str):
                    try:
                        buff = msg.encode('utf-8')
                        msg = buff
                    except:
                        pass
                bSz += len(msg)
            b += struct.pack('Q', bSz)

            if (level != None):
                lvl = int(level)
                b += struct.pack('Q', lvl)

            if (msg != None):
                b += msg
            return b



        # publishFromFile - Publish a module from a file
        #   TODO:  Convert this to PACK / Message interface
        #---------------------------------------------------------------------
        def publishFromFile(self, module, meta):
            self._masLog.debug('MAS2py.publishFromFile()')
            self._masLog.debug('  module: '+str(module))
            self._masLog.debug('  meta: '+str(meta))
            rc = 0
            meth = {}
            invCache = False
            try:
                up = None
                while (not up):
                    try:
                        # Check to see if we have loaded a module with this name before
                        # if not then import it, otherwise we need to reload it
                        if module not in sys.modules:
                            up =  __import__(module)
                        else:
                            # Reload with recompile ('versioning')
                            pycFile = os.path.join(masTmpPath, module+'.pyc')
                            if (os.path.exists(pycFile)):
                                os.remove(pycFile)
                            up = reload(sys.modules[module])
                            self._masLog.debug('  publish module: '+str(module))
                    except ImportError as exception:
                        modFilename = os.path.join(masTmpPath, module+'.py')
                        exists = os.path.isfile(modFilename)
                        if (invCache or (not exists)):
                            tb = traceback.format_exc()
                            msg = '  ***** import('+str(module)+') Exception: '+str(sys.exc_info()[0])+':\n'+str(tb)
                            raise masException(msg)
                        try:
                            invalidate_caches()
                        except:
                            pass
                        invCache = True
                        sleep(0.1)
                    except Exception as exception:
                        tb = traceback.format_exc()
                        msg = '  ***** publish('+str(module)+') Exception: '+str(sys.exc_info()[0])+':\n'+str(tb)
                        raise masException(msg)

                self._masLog.debug('  module getmembers')
                x  = insp.getmembers(up, insp.isroutine)
                for i in x:
                    isBuiltin = isinstance(i[1], types.BuiltinFunctionType)
                    if (isBuiltin):
                        continue
                    uf = op.attrgetter(i[0])
                    doc = insp.getdoc(uf(up))
                    if ((doc is None) or not(doc.lower().startswith('output:'))):
                        continue
                    doc = doc[7:].split(',')
                    doc[0] = doc[0].lstrip().rstrip()
                    if not doc[0]:
                        doc = []
                    try:
                        try:
                            args = insp.getfullargspec(uf(up)).args
                        except:
                            args = insp.getargspec(uf(up)).args
                    except:
                        continue
                    meth[i[0]] = [uf, args, doc]
                    self.ups[module] = [up, meth]

                ## Package the Metadata
                self._masLog.debug('---  meta')
                if meta:
                    self._masLog.debug('  publishFromFile: MetaData')
                    retPack = struct.pack('i', len(meth))
                    for func in meth.keys():
                        # Process method name/length
                        funcEnc = func.encode()
                        retPack += struct.pack('i', len(funcEnc))
                        retPack += funcEnc

                        # Processes Method arguments
                        args = meth.get(func)
                        inArgs = args[1]
                        outArgs = args[2]
                        retPack += struct.pack('i', len(inArgs))
                        retPack += struct.pack('i', len(outArgs))

                        # For each input arg add name length and name to out
                        for inA in inArgs:
                            name = inA.strip()
                            nameE = name.encode()
                            retPack += struct.pack('i', len(nameE))
                            retPack += nameE

                        # For each output arg add name length and name to out
                        for outA in outArgs:
                            name = outA.strip()
                            nameE = name.encode()
                            retPack += struct.pack('i', len(nameE))
                            retPack += nameE

                    # Send the Metadata
                    retPack = self.packReturnMsg(MASCmd_Publish, retPack)
                    self.write(retPack)

            except masException:
                raise
            except:
                tb = traceback.format_exc()
                msg = '  ***** publishFromFile: Exception\n'+str(tb)
                self._masLog.error(msg, mas=False)
                raise masException(msg)
            self._masLog.debug('  publishFromFile: Published')
            return True



        # dt1960to1970() - DateTime from 1960 -> 1970
        #---------------------------------------------------------------------
        def dt1960to1970(self, millisecondsSince1960):
            date1960 = datetime(1960, 1, 1)
            delta1960 = timedelta(milliseconds=millisecondsSince1960)
            retVal = (date1960 + delta1960)
            return retVal

        # dt1970to1960() - DateTime from 1970 -> 1960
        #---------------------------------------------------------------------
        def dt1970to1960(self, pythonDT):
            millisecondsSince1960 = 0
            if (type(pythonDT) == datetime):
                millisecondsSince1960 = calendar.timegm(pythonDT.utctimetuple())
            else:
                millisecondsSince1960 = calendar.timegm(pythonDT.timetuple())
            millisecondsSince1960 = millisecondsSince1960 * 1000
            if (type(pythonDT) == datetime):
                millisecondsSince1960 = millisecondsSince1960 + (pythonDT.microsecond // 1000)
            millisecondsSince1960 = millisecondsSince1960 + 315619200000
            return millisecondsSince1960



        #  unpackArg() - convenience Routine for unpacking arguments
        #---------------------------------------------------------------------
        def unpackArg(self, args, idx, type, size):
            self._masLog.trace('      -- unpackArg() idx:'+str(idx)+', type: '+str(type)+', size: '+str(size))
            buff = args[idx:(idx+size)]
            if (len(buff) != size):
                msg = 'Invalid argument buffer size:  len('+str(len(buff))+') != ('+str(size)+')'
                raise masException(msg)
            val, = struct.unpack(type, buff)
            idx += size
            self._masLog.trace('      -- unpackArg() -- idx: '+str(idx)+' : '+str(val))
            return (val, idx)

        # unpackArray(): note: Does not handle array of arrays [[],[],[]]
        #---------------------------------------------------------------------
        def unpackArray(self, b, pyFmt, valSz):
            la = []
            idx = 4
            cnt, = struct.unpack('i', b[:idx])
            for _ in range(cnt):
                c, = struct.unpack('c', b[idx:idx+1])
                idx += 1
                if (c == 'n'):
                    la.append(None)
                else:
                    val, = struct.unpack(pyFmt, b[idx:idx+valSz])
                    la.append(val)
                    idx += valSz
            return (b[idx:], la)


        # Process unpacking an argument buffer into a Python List
        #---------------------------------------------------------------------
        def unpackArguments(self, argsB, nArgsIn):
            args = []
            idx = 0
            for argsCnt in range(nArgsIn):
                # Argument type
                (dType, idx) = self.unpackArg(argsB, idx, 'c', 1)

                # Missing
                if (dType == b'n'):
                    args.append(None)
                elif (dType == b'N'):
                    self._masLog.trace('   -- None array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (ch, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        # Even if ch is not 'n', we still append None.
                        aVal.append(None)
                    args.append(aVal)

                # Boolean
                elif (dType == b'1'):
                    self._masLog.trace('   -- True')
                    args.append(True)
                elif (dType == b'0'):
                    self._masLog.trace('   -- False')
                    args.append(False)
                elif (dType == b'B'):
                    self._masLog.trace('   -- bool array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (bVal, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (bVal == b'n'):
                            bVal = None
                        elif (bVal == b'0'):
                            bVal = False
                        else:
                            bVal = True
                        aVal.append(bVal)
                    args.append(aVal)

                # Integer
                elif (dType == b'i'):
                    self._masLog.trace('   -- int')
                    (iVal, idx) = self.unpackArg(argsB, idx, 'i', 4)
                    args.append(iVal)
                elif (dType == b'I'):
                    self._masLog.trace('   -- int array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (ch, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (ch == b'n'):
                            aVal.append(None)
                        else:
                            (iVal, idx) = self.unpackArg(argsB, idx, 'i', 4)
                            aVal.append(iVal)
                    args.append(aVal)

                # Long
                elif (dType == b'l'):
                    self._masLog.trace('   -- long')
                    (lVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                    args.append(lVal)
                elif (dType == b'L'):
                    self._masLog.trace('   -- long array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (ch, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (ch == b'n'):
                            aVal.append(None)
                        else:
                            (lVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                            aVal.append(lVal)
                    args.append(aVal)

                # Double
                elif (dType == b'f'):
                    self._masLog.trace('   -- double')
                    (dVal, idx) = self.unpackArg(argsB, idx, 'd', 8)
                    args.append(dVal)
                elif (dType == b'F'):
                    self._masLog.trace('   -- double array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (ch, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (ch == b'n'):
                            aVal.append(None)
                        else:
                            (dVal, idx) = self.unpackArg(argsB, idx, 'd', 8)
                            aVal.append(dVal)
                    args.append(aVal)

                # Date
                elif (dType == b'd'):
                    self._masLog.trace('   -- date')
                    (qVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                    dVal = self.dt1960to1970(qVal)
                    dt = dVal.date()
                    self._masLog.trace('   -- date type: '+str(type(dt)))
                    args.append(dt)
                elif (dType == b'D'):
                    self._masLog.trace('   -- date array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (ch, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (ch == b'n'):
                            aVal.append(None)
                        else:
                            (qVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                            dVal = self.dt1960to1970(qVal)
                            dt = dVal.date()
                            aVal.append(dt)
                    args.append(aVal)

                # Time
                elif (dType == b't'):
                    self._masLog.trace('   -- time')
                    (qVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                    self._masLog.trace('   -- time: raw: '+str(qVal))
                    dVal = datetime.utcfromtimestamp(qVal//1000).replace(microsecond=qVal%1000*1000).timetz()
                    self._masLog.trace('   -- time in: '+str(dVal))
                    self._masLog.trace('   -- time type: '+str(type(dVal)))
                    args.append(dVal)
                elif (dType == b'T'):
                    self._masLog.trace('   -- time array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (ch, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (ch == b'n'):
                            aVal.append(None)
                        else:
                            (qVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                            dVal = datetime.utcfromtimestamp(qVal//1000).replace(microsecond=qVal%1000*1000).timetz()
                            aVal.append(dVal)
                    args.append(aVal)

                # C-Time
                elif (dType == b'm'):
                    self._masLog.trace('   -- C-Time')
                    (qVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                    dVal = self.dt1960to1970(qVal)
                    self._masLog.trace('   -- CTime type: '+str(type(dVal)))
                    args.append(dVal)
                elif (dType == b'M'):
                    self._masLog.trace('   -- C-Time array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (ch, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (ch == b'n'):
                            aVal.append(None)
                        else:
                            (qVal, idx) = self.unpackArg(argsB, idx, 'q', 8)
                            dVal = self.dt1960to1970(qVal)
                            aVal.append(dVal)
                    args.append(aVal)

                # String
                elif (dType == b's'):
                    self._masLog.trace('   -- string ++')
                    sLen = argsB[idx:].index(null)
                    self._masLog.trace('   -- string len: '+str(sLen))
                    sType = str(sLen) + 's'
                    self._masLog.trace('   -- string len: '+str(sLen))
                    (bVal, idx) = self.unpackArg(argsB, idx, sType, sLen)
                    sVal = bVal.decode("utf-8")
                    self._masLog.trace('   -- string type: '+str(type(sVal)))
                    args.append(sVal)
                    (_, idx) = self.unpackArg(argsB, idx, 'c', 1)
                elif (dType == b'S'):
                    self._masLog.trace('   -- string array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (sCh, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (sCh == b'n'):
                            aVal.append(None)
                        elif (sCh == b's'):
                            sLen = argsB[idx:].index(null)
                            self._masLog.trace('   -- string len: '+str(sLen))
                            sType = str(sLen) + 's'
                            (bVal, idx) = self.unpackArg(argsB, idx, sType, sLen)
                            sVal = bVal.decode("utf-8")
                            aVal.append(sVal)
                            (_, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        else:
                            raise masException('Invalid string identifier')
                    args.append(aVal)

                # BLOB
                elif (dType == b'o'):
                    self._masLog.trace('   -- BLOB ++')
                    (blobSz, idx) = self.unpackArg(argsB, idx, 'q', 8)
                    self._masLog.trace('   -- BLOB size: '+str(blobSz))
                    sType = str(blobSz) + 's'
                    (bVal, idx) = self.unpackArg(argsB, idx, sType, blobSz)
                    self._masLog.trace('   -- BLOB type: '+str(type(bVal)))
                    args.append(bVal)

                elif (dType == b'O'):
                    #masLog.debug('   -- BLOB array')
                    (aCnt, idx) = self.unpackArg(argsB, idx, 'I', 4)
                    aVal = []
                    for _ in range(aCnt):
                        (oCh, idx) = self.unpackArg(argsB, idx, 'c', 1)
                        if (oCh == b'n'):
                            aVal.append(None)
                        elif (oCh == b'o'):
                            (blobSz, idx) = self.unpackArg(argsB, idx, 'q', 8)
                            #masLog.debug('   -- BLOB len: '+str(blobSz))
                            sType = str(blobSz) + 's'
                            (oVal, idx) = self.unpackArg(argsB, idx, sType, blobSz)
                            aVal.append(oVal)
                        else:
                            raise masException('Invalid BLOB identifier')
                    args.append(aVal)

            return args


        # argTypeCh() - Return the argument processing type MAS Byte
        #---------------------------------------------------------------------
        def argTypeCh(self, val):
            if (val is None):
                return b'n'
            vType = type(val)
            if (vType is bool):
                return b'b'
            elif (vType in (int, long)):
                return b'l'
            elif (vType is float):
                return b'f'
            elif (vType is date):
                return b'd'
            elif (vType is time):
                return b't'
            elif (vType is datetime):
                return b'm'
            elif (vType in (str, unicode)):
                return b's'
            elif (vType is bytes):
                return b'o'
            else:
                msg = 'Processing Return Argument:  Invalid type('+str(vType)+')'+', value('+str(val)+')'
                raise masException(msg)


        #  packArg() - convenience Routine for packing arguments
        #  NOTE:  String:  C->Py:buff,  Py->C:Null-Terminated
        #---------------------------------------------------------------------
        def packArg(self, masCh=None, val=None):
            # Output MAS Type Byte
            if ((type(val) is float) and (math.isnan(val))):
                val = None
            if ((masCh is None) or (val is None)):
                masCh = self.argTypeCh(val)
            lBuff = struct.pack('c', masCh)
            if (not val is None):
                if (masCh == b'b'):
                    lBuff += struct.pack('?', val)
                elif (masCh == b'l'):
                    try:
                        lBuff += struct.pack('q', val)
                    except:
                        # TO-DO: output Module.Method() names
                        msg = 'Integer Argument Overflowed.  Value: '+str(val)
                        raise masException(msg)
                elif (masCh == b'f'):
                    lBuff += struct.pack('d', val)
                elif (masCh in (b'd', b'm')):
                    iDate = int(self.dt1970to1960(val))
                    lBuff += struct.pack('q', iDate)
                elif (masCh == b't'):
                    dt = datetime(1970, 1, 1, val.hour, val.minute, val.second)
                    iTime = int((calendar.timegm(dt.utctimetuple())*1000) + val.microsecond // 1000)
                    lBuff += struct.pack('q', iTime)
                elif (masCh == b's'):
                    try:
                        sBuff = val.encode('utf-8')
                    except:
                        sBuff = val
                    sBuff += struct.pack('?',0)   # Null terminate
                    sSz = len(sBuff)
                    sFmt = str(sSz) + 's'
                    lBuff += struct.pack('i', sSz)
                    lBuff += struct.pack(sFmt, sBuff)
                elif (masCh == b'o'):
                    blobSz = len(val)
                    sFmt = str(blobSz) + 's'
                    lBuff += struct.pack('q', blobSz)
                    lBuff += struct.pack(sFmt, val)
                else:
                    # TO-DO: output Module.Method() names
                    msg = 'Packing Return Argument:  Invalid type('+str(vType)+')'+', value('+str(val)+')'
                    raise masException(msg)
            return lBuff


        # packArray() - convenience Routine for packing arrays
        #---------------------------------------------------------------------
        def packArray(self, array):
            # determine Element type
            aVal = None
            if not (array is None):
                for val in array:
                    if (val is None):
                        continue
                    if ((type(val) is float) and (math.isnan(val))):
                        continue
                    aVal = val
                    break

            # Determine Element type characters
            if (aVal is None):
                lBuff = struct.pack('c', b'N')
                lBuff += struct.pack('i', len(array))
            else:
                masCh = self.argTypeCh(aVal)
                uc = masCh.upper()
                cnt = len(array)
                lBuff = struct.pack('c', uc)
                lBuff += struct.pack('i', cnt)
                for val in array:
                    if ((type(val) is float) and (math.isnan(val))):
                        val = None
                    lBuff += self.packArg(masCh, val)
            return lBuff


        # packReturnArgs() - Package the arguments into a buffer
        def packReturnArgs(self, retArgs):
            self._masLog.trace('  packReturnArgs: '+str(retArgs))
            if (retArgs is None):
                lBuff = None
            elif (type(retArgs) is tuple):
                lBuff = b''
                for rVal in retArgs:
                    if (type(rVal) == list):
                        lBuff += self.packArray(rVal)
                    else:
                        if (rVal is None):
                            lBuff += self.packArg()
                        else:
                            masCh = self.argTypeCh(rVal)
                            lBuff += self.packArg(masCh, rVal)
            else:
                msg = '  Invalid Argument: value('+str(args)+'), type('+str(type(args))+')'
                raise masException(msg)
            return lBuff




        # invoke() - Excute the published module:  Fun.mod(args)
        #----------------------------------------------------------------------
        def invoke(self, payload):
            self._masLog.debug('MAS2py.invoke(seqID='+str(self._seqID)+')')
            try:
                # Process the invoke datagram
                headOff = 16
                (nArgsIn, nArgsOut, modL, funcL) = struct.unpack('IIII', payload[:headOff])
                self._masLog.trace(' -- nArgsIn('+str(nArgsIn)+')')
                self._masLog.trace(' -- nArgsOut('+str(nArgsOut)+')')
                self._masLog.trace(' -- modL('+str(modL)+')')
                self._masLog.trace(' -- funcL('+str(funcL)+')')

                # Read the variable buffers
                modB  = payload[headOff:(headOff+modL)]
                headOff += modL
                funcB = payload[headOff:(headOff+funcL)]
                headOff += funcL

                # utf-8 processing
                mod  = modB.decode('utf-8', 'replace')
                #self._masLog.debug('   -- modName:  '+str(mod))
                func = funcB.decode('utf-8', 'replace')
                #self._masLog.debug('   -- funcName: '+str(func))

                # Process the Arguments
                argsB = payload[headOff:]
                args = self.unpackArguments(argsB, nArgsIn)

                # Invoke the method
                self._masLog.debug('  '+str(mod)+'.'+str(func)+'('+str(args)+')')
                up  = self.ups.get(mod)
                try:
                    out = up[1].get(func)[0](up[0])(*args)
                except:
                    tb = traceback.format_exc()
                    msg = str(tb)
                    raise masException(msg)
                self._masLog.debug('      ==> '+str(out))

                # Validate expected number of Argument outputs
                #self._masLog.debug('  -- Validate count of return arguments')
                if ((pd is None) or not (type(out) is pd.core.frame.DataFrame)):
                    if (out is None):
                        if (nArgsOut == 1):
                            # None translates into missing value
                            out = (out,)
                            numOut = 1
                        else:
                            numOut = 0
                    else:
                        # Promote non-tuple types
                        if (not (type(out) is tuple)):
                            out = (out,)
                        if ((nArgsOut == 1) and (len(out) == 0)):
                            out = (None,)
                        numOut = len(out)

                # Validated Expected number of arguments
                if (nArgsOut != numOut):
                    msg = 'invoke: '+mod+'.'+func+'(): Output Arg Count(' + str(numOut) + ') does not match expected(' + str(nArgsOut) +
                    raise masException(msg)

                # Pack return values
                self._masLog.debug('invoke: '+str(func)+'('+str(args)+') => '+str(out))
                retArgs = self.packReturnArgs(out)

                # Generate return package / send
                retPack = self.packReturnMsg(MASCmd_Invoke, retArgs)
                self.write(retPack)


            except KeyboardInterrupt:
                self._masLog.info('invoke: Keyboard Interrupt')
                pass
            except masException:
                raise
            except:
                tb = traceback.format_exc()
                msg = '  **** invoke: Exception\n'+str(tb)
                raise masException(msg)
            self._masLog.debug('MAS2py.invoke() -- end')
            return
        #--  invoke()  -------------------------------------------------------






    ##########################################################################
    # main() - Main Command Loop
    ##########################################################################
    def main():
        try:
            # Instantiate MAS instance
            mas = MAS2py()

            # Acknowledge
            sys.stdout.write('MAS_ok')
            sys.stdout.flush()
            auth = os.read(0,16)

            # Setup STDIN, STDOUT, STDERR
            outName = getEnv('MAS_PYOUT_FILE')
            outFile = None
            fmode = 'w'
            if (outName):
                try:
                    if (outName[0] == '+'):
                        fmode = 'a'
                        outName = outName[1:]
                    outFile = open(outName, fmode)
                except:
                    outFile = None
            if (outFile is None):
                outFile = open(os.devnull, 'w')
            inFile = open(os.devnull, 'r')
            sys.stdin.close()
            sys.stdout.close()
            sys.stderr.close()
            sys.stdin = inFile
            sys.stdout = outFile
            sys.stderr = outFile
            print("*************")

            # Process command line arguments
            try:
                exe  = sys.argv[0]
                host = sys.argv[1]
                port = sys.argv[2]
            except:
                msg = 'MAS2Py Invalid command line: ['
                for arg in sys.argv:
                    msg += arg + ','
                msg += ']'
                print(msg)
                mas._masLog.fatal(msg)
                return -1

            # Setup Temp Path
            global masTmpPath
            masTmpPath = tempfile.mkdtemp()
            sys.path.insert(0, masTmpPath)

            # Connect to MAS Server
            try:
                mas.connect(host, int(port), auth)
            except:
                raise

            # Log Startup
            now = datetime.now()
            mas._masLog.info('--------------------------------------------------------------------------')
            mas._masLog.info('    MAS Python Interface started '+str(now))
            mas._masLog.info('    Python Version '+str(platform.python_version()))
            mas._masLog.info('    mas2py Version '+ MAS2PY_VERSION)
            mas._masLog.info('--------------------------------------------------------------------------')
            mas._masLog.info('                 exe: '+exe)
            mas._masLog.info('                host: '+host)
            mas._masLog.info('                port: '+port)
            mas._masLog.info('             tmpPath: '+masTmpPath)
            mas._masLog.info('--------------------------------------------------------------------------')

            # Command Loop
            mas._masLog.debug('Entering command loop')
            loop = True
            cnt = 0
            while loop:
                try:
                    # Receive the header
                    cmdHeader = mas.read(12)
                    mas._masLog.trace('cmdHeader: '+str(cmdHeader))
                    cmd = struct.unpack('I', cmdHeader[:4])[0]
                    opCode = ((cmd >> 24) & 0xff)
                    seqID = (cmd & 0x00ffffff)
                    mas._seqID = seqID
                    payloadSz = struct.unpack('Q', cmdHeader[4:])[0]
                    mas._masLog.trace('cmdLoop: opCode('+str(opCode)+'), seqID('+str(seqID)+'), payloadSz('+str(payloadSz)+')')

                    cnt = cnt + 1
                    if (opCode == MASCmd_Publish):
                        # TODO: Move to Publish
                        # Read the datagram
                        mas._masLog.trace('cmdLoop: mas.publish')
                        meta = struct.unpack('i', mas.read(4))[0]
                        modl = struct.unpack('i', mas.read(4))[0]
                        modB = mas.read(modl)
                        code = mas.read(payloadSz)

                        # Create the temporary file
                        mod = modB.decode('utf-8', 'replace')
                        modFilename = os.path.join(masTmpPath, mod+'.py')
                        mas._masLog.trace('    publish: '+str(mod)+' -> '+modFilename)
                        try:
                            with open(modFilename, mode='wb', buffering=0) as mas.f1:
                                mas.f1.write(code)
                        except:
                            tb = traceback.format_exc()
                            msgS = str(tb)
                            i = msgS.find('IOError:')
                            if (i > 0):
                                j = msgS.find(':', (i+8))
                                if (j > 0):
                                    msgS = msgS[:j] + '\n'
                            raise masException(msgS)

                        # Publish the module
                        mas.publishFromFile(mod, meta)
                        mas._masLog.trace('cmdLoop: mas.publish() -- end')

                    elif (opCode == MASCmd_PublishFile):
                        # TODO:  FIX THE ACTUAL SENT PACKET
                        # Read the datagram
                        mas._masLog.trace('cmdLoop: mas.publishFromFile() start')
                        modl = struct.unpack('i', mas.read(4))[0]
                        meta = struct.unpack('i', mas.read(4))[0]
                        modB = mas.read(modl)

                        # utf-8 processing
                        mod = modB.decode('utf-8', 'replace')

                        # Publish the module
                        rc = mas.publishFromFile(mod, meta)
                        mas._masLog.trace('cmdLoop: mas.publishFromFile() end')

                    elif (opCode == MASCmd_Invoke):
                        # invoke the module/function
                        mas._masLog.trace('cmdLoop: mas.invoke() start')
                        payload = mas.read(payloadSz)
                        mas.invoke(payload)
                        mas._masLog.trace('cmdLoop: mas.invoke() end')

                    elif (opCode == MASCmd_Version):
                        # Python version string
                        mas._masLog.trace('cmdLoop: Python Version')
                        msg = 'Running Python Version ' + str(platform.python_version()) + ' on (host:port) ' + str(host) + ':'+ str(por
                        ln = len(msg.encode())
                        mas._masLog.trace(msg)
                        b = struct.pack('q', ln)
                        mas.write(b)
                        b = msg.encode()
                        mas.write(b)
                        mas._masLog.trace('cmdLoop: mas.version() end')

                    elif (opCode == MASCmd_Shutdown):
                        # Shutdown
                        mas._masLog.trace('cmdLoop: Python Shutdown')

                        # Clean up temp dir and files
                        shutil.rmtree(masTmpPath, ignore_errors=False)
                        masTmpPath = None
                        loop = False

                        # Shutdown stdout
                        sys.stdout.close()

                        # Shutdown message
                        retPack = mas.packReturnMsg(MASCmd_Shutdown)
                        mas.write(retPack)

                    else:
                        # Invalid opCode
                        msg = 'cmdLoop: Invalid opCode('+str(opCode)+')'
                        mas._masLog.critical(msg)
                        raise masException(msg)

                    # TODO: Process Logs
                    # Process Complete
                    mas._masLog.debug('cmdLoop: Complete')
                    retPack = mas.packReturnMsg(MASCmd_Complete)
                    mas.write(retPack)

                except KeyboardInterrupt:
                    mas._masLog.debug('cmdLoop: Keyboard Interrupt')
                    print(msgS)
                    pass
                except masException as msg:
                    msgS = str(msg)
                    print(msgS)
                    mas._masLog.error(msgS, mas=False)
                    retPack = mas.packReturnMsg(MASCmd_Exception, msgS)
                    mas.write(retPack)
                except:
                    tb = traceback.format_exc()
                    msgS = str(tb)
                    print(msgS)
                    mas._masLog.fatal(msgS, mas=False)
                    retPack = mas.packReturnMsg(MASCmd_Exception, msgS)
                    try:
                        mas.write(retPack)
                    except:
                        pass
                    raise masException('Main Processing Loop Exception')
        except:
            tb = traceback.format_exc()
            msgS = str(tb)
            print(msgS)
            mas._masLog.fatal(msgS)
            pass

        # Cleanup the temporary directory
        if (not masTmpPath is None):
            shutil.rmtree(masTmpPath, ignore_errors=True)
            masTmpPath = None

    if __name__ == "__main__":
        main()
    ;;;;
    run;quit;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
