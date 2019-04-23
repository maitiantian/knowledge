<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a href="javascript:void(0)" style="color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# supervisor

[supervisor官方文档](http://supervisord.org/)

supervisor，进程管理工具。

* 简单
    > supervisor通过fork/exec方式把被管理的进程，当作supervisor的子进程来启动。我们只需把要管理的进程的可执行文件的路径写进在supervisor的配置文件中。被管理进程作为supervisor的子进程，子进程挂掉的时，父进程可以获取子进程挂掉的信息，也可以对挂掉的子进程进行自动重启。
* 精确
    > linux对进程状态的反馈，有时不太准确。而supervisor监控子进程，得到的子进程状态是准确的。
* 进程组
    > supervisor可以对进程组统一管理，也就是说可以把需要管理的进程写到一个组里，然后把这个组作为一个对象进行管理，如启动，停止，重启等等操作。而linux系统没有这种功能，想要停止一个进程，只能一个一个去停止，或者写脚本批量停止。
* 可扩展性
    > supervisor是个开源软件。supervisor主要提供了两个可扩展的功能。event机制和xml_rpc。
* 权限
    > linux的进程，特别是侦听在1024端口下的进程，一般用户大多数情况下，是不能对其进行控制的。想要控制必须有root权限。而supervisor提供了一个功能，可以为supervisord或者每个子进程，设置一个非root的user，这个user可以管理它对应的进程。

```bash
[unix_http_server]            
file=/tmp/supervisor.sock   ; socket文件的路径，supervisorctl用XML_RPC和supervisord通信就是通过它进行的，
                              如果不设置，supervisorctl就不能用，
                              默认为none，非必须设置。
;chmod=0700                 ; 修改上面的那个socket文件的权限为0700，
                              默认为0700，非必须设置。
;chown=nobody:nogroup       ; 修改上面的那个socket文件的属组为user.group，
                              默认为启动supervisord进程的用户及属组，非必须设置，
;username=user              ; 使用supervisorctl连接的时候，认证的用户
                              默认为不需要用户，非必须设置。
;password=123               ; 和上面的用户名对应的密码，可以直接使用明码，也可以使用SHA加密，
                              如：{SHA}82ab876d1387bfafe46cc1c8a2ef074eae50cb1d
                              默认不设置，非必须设置。

;[inet_http_server]         ; 侦听在TCP上的socket，Web Server和远程的supervisorctl都要用到它，
                              默认为不开启，非必须设置。
;port=127.0.0.1:9001        ; 侦听的IP和端口，侦听所有IP用:9001或*:9001，
                              只要上面的[inet_http_server]开启了，就必须设置它。
;username=user              ; 和上面的uinx_http_server一样，非必须设置。
;password=123               ; 同上，非必须设置。

[supervisord]                ; 定义supervisord这个服务端进程的一些参数，
                               必须设置，不设置，supervisor就无法工作了。
logfile=/tmp/supervisord.log ; supervisord这个主进程的日志路径，和子进程的日志无关，
                               默认路径$CWD/supervisord.log，$CWD是当前目录，非必须设置。
logfile_maxbytes=50MB        ; 上面那个日志文件的最大大小，超过50M时，会生成一个新的日志文件，
                               当设置为0时，不限制文件大小，默认值是50M，非必须设置。              
logfile_backups=10           ; 日志文件数量，上面的日志文件大于50M时，会生成一个新文件，
                               文件数量大于10时，最初的老文件被新文件覆盖，文件数量将保持为10，
                               当设置为0时，不限制文件的数量，默认为10，非必须设置。
loglevel=info                ; 日志级别，有critical，error，warn，info，debug，trace，blather等，
                               默认为info，非必须设置。
pidfile=/tmp/supervisord.pid ; supervisord的pid文件路径；
                               默认为$CWD/supervisord.pid，非必须设置。
nodaemon=false               ; 如果是true，supervisord进程将在前台运行，
                               默认为false，supervisord进程在后台以守护进程运行，非必须设置。
minfds=1024                  ; 这个是最少系统空闲的文件描述符，低于这个值supervisor将不会启动，
                               系统的文件描述符在这里设置，cat /proc/sys/fs/file-max，
                               默认为1024，非必须设置。
minprocs=200                 ; 最小可用的进程描述符，低于这个值supervisor也不会正常启动，
                               ulimit -u这个命令，可以查看linux下面用户的最大进程数，
                               默认为200，非必须设置。
;umask=022                   ; 进程创建文件的掩码，
                               默认为022，非必须设置。
;user=chrism                 ; 设置一个非root用户，当我们以root用户启动supervisord之后，
                               这里设置的这个用户，也可以对supervisord进行管理，
                               默认不设置，非必须设置。
;identifier=supervisor       ; supervisord的标识符，主要给XML_RPC用，
                               当有多个supervisor的时候，想调用XML_RPC统一管理，需要为每个supervisor设置不同标识符，
                               默认是supervisord，非必需设置。
;directory=/tmp              ; supervisord作为守护进程运行的时候，启动supervisord进程之前，会先切换到这个目录，
                               默认不设置，非必须设置。
;nocleanup=true              ; 为false时，会在supervisord进程启动时，
                               把以前子进程产生的日志文件（路径为AUTO的情况下）清除掉，
                               默认是false，有调试需求的可以设置为true，非必须设置。
;childlogdir=/tmp            ; 子进程日志路径为AUTO时，子进程日志文件的存放路径，
                               默认为/tmp，执行下面命令可查看：
                               python -c "import tempfile;print tempfile.gettempdir()"
                               非必须设置。
;environment=KEY="value"     ; 设置环境变量，supervisord在linux中启动默认继承了linux的环境变量，
                               这里可以设置supervisord进程特有的其他环境变量，
                               supervisord启动子进程时，子进程会拷贝父进程的内存空间内容，
                               所以设置的这些环境变量也会被子进程继承。
                               例：environment=name="haha",age="hehe"
                               默认不设置，非必须设置。
;strip_ansi=false            ; 如果设置为true，会清除子进程日志中的所有ANSI序列。
                               什么是ANSI序列？就是我们的\n，\t这些东西。
                               默认为false，非必须设置。

; the below section must remain in the config file for RPC
; (supervisorctl/web interface) to work, additional interfaces may be
; added by defining them in separate rpcinterface: sections

[rpcinterface:supervisor]    ; 这个选项是给XML_RPC用的，如果想使用supervisord或者web server，这个选项必须开启
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface 

[supervisorctl]              ; 针对supervisorctl的一些配置  
serverurl=unix:///tmp/supervisor.sock ; supervisorctl本地连接supervisord时，本地UNIX socket路径，
                                        这个是和前面的[unix_http_server]对应的，
                                        默认值是unix:///tmp/supervisor.sock，非必须设置。
;serverurl=http://127.0.0.1:9001 ; supervisorctl远程连接supervisord时，用到的TCP socket路径，
                                   这个和前面的[inet_http_server]对应，
                                   默认是http://127.0.0.1:9001，非必须设置。
                               
;username=chris              ; 用户名，
                               默认空，非必须设置。
;password=123                ; 密码
                               默认空，非必须设置。
;prompt=mysupervisor         ; 输入用户名密码时的提示符
                               默认supervisor，非必须设置。
;history_file=~/.sc_history  ; 和shell中的history类似，我们可以用上下键来查找前面执行过的命令，
                               默认是no file，如果我们想要有这种功能，必须指定一个文件，非必须设置。

; The below sample program section shows all possible program subsection values,
; create one or more 'real' program: sections to be able to control them under
; supervisor.

;[program:theprogramname]      ; 要管理的子进程，":"后面是名字，别乱写和实际进程有点关联最好。
                                 这样的program我们可以设置一个或多个，一个program就是一个要被管理的进程。
;command=/bin/cat              ; 要启动进程的路径、命令，可以带参数，
                                 例：/home/test.py -a 'hehe'。
                                 command只能是那种在终端运行的进程，不能是守护进程，
                                 比如说command=service httpd start，
                                 httpd这个进程被linux的service管理了，
                                 supervisor再去启动这个命令这已经不是严格意义的子进程了。
                                 这个是必须设置项。
;process_name=%(program_name)s ; 进程名，如果下面的numprocs参数为1的话，就不用管这个参数了，
                                 默认值%(program_name)s就是上面的那个program冒号后面的名字，
                                 如果numprocs为多个的话，那就不能这样了，不可能每个进程都用同一个进程名。

                                
;numprocs=1                    ; 启动进程的数目。不为1时，就是进程池的概念，
                                 默认为1，非必须设置。
;directory=/tmp                ; 进程运行前，会前切换到这个目录
                                 默认不设置，非必须设置。
;umask=022                     ; 进程掩码，默认none，非必须设置。
;priority=999                  ; 子进程启动、关闭优先级，优先级低的，最先启动，关闭时最后关闭，
                                 默认值为999，非必须设置。
;autostart=true                ; 如果是true的话，子进程将在supervisord启动后被自动启动，
                                 默认为true，非必须设置。
;autorestart=unexpected        ; 设置子进程挂掉后自动重启的情况，有三个选项，false，unexpected和true。
                                 如果为false，无论什么情况都不会被重新启动，
                                 如果为unexpected，只有当进程的退出码不在下面的exitcodes里面定义时才会被自动重启，
                                 为true时，只要子进程挂掉就会被无条件的重启。
;startsecs=1                   ; 子进程启动多少秒之后，如果状态是running，则认为启动成功。
                                 默认值为1，非必须设置。
;startretries=3                ; 当进程启动失败后，最大尝试启动的次数，
                                 当超过次数后，supervisor将把此进程的状态置为FAIL。
                                 默认值为3，非必须设置。
;exitcodes=0,2                 ; 注意和上面的的autorestart=unexpected对应，exitcodes里面的定义的退出码是expected的。
;stopsignal=QUIT               ; 进程停止信号，可以为TERM，HUP，INT，QUIT，KILL，USR1，USR2等信号。
                                 默认为TERM，用设定的信号去干掉进程时，退出码会被认为是expected，非必须设置。
;stopwaitsecs=10               ; 向子进程发送stopsignal信号后，到系统返回信息给supervisord，所等待的最大时间。
                                 超过这个时间，supervisord会向该子进程发送一个强制kill的信号。
                                 默认为10秒，非必须设置。
;stopasgroup=false             ; supervisord管理的子进程本身还有子进程时，如果仅仅干掉supervisord的子进程的话，
                                 子进程的子进程可能会变成孤儿进程。所以可以设置可个选项，把该子进程的整个进程组都干掉。
                                 如果设置为true，一般killasgroup也会被设置为true。
                                 该选项发送的是stop信号，默认为false，非必须设置。
;killasgroup=false             ; 和上面的stopasgroup类似，发送的是kill信号。
;user=chrism                   ; 如果supervisord是root启动，我这里设置的非root用户，可以用来管理该program。
                                 默认不设置，非必须设置。
;redirect_stderr=true          ; 如果为true，则stderr的日志会被写入stdout日志文件中。
                                 默认为false，非必须设置。
;stdout_logfile=/a/path        ; 子进程的stdout的日志路径，可以指定路径，AUTO，none等三个选项。
                                 设置为none，将没有日志产生，
                                 设置为AUTO，将随机找个地方生成日志，且当supervisord重启时，以前的日志文件会被清空。
                                 redirect_stderr=true时，sterr也会写进这个日志文件。
;stdout_logfile_maxbytes=1MB   ; 日志文件最大大小，和[supervisord]中定义的一样。默认50M。
;stdout_logfile_backups=10     ; 和[supervisord]中定义的一样。默认10。
;stdout_capture_maxbytes=1MB   ; 设定capture管道的大小，值不为0时，子进程可以从stdout发送信息，
                                 而supervisor可以根据信息，发送相应的event。
                                 默认为0，为0的时候表示关闭管道，非必须设置。
;stdout_events_enabled=false   ; 为ture时，当子进程由stdout向文件描述符中写日志时，
                                 将触发supervisord发送PROCESS_LOG_STDOUT类型的event。
                                 默认为false，非必须设置。
;stderr_logfile=/a/path        ; 设置stderr的日志路径，redirect_stderr=true时这个就不用设置了，
                                 设置了也没用，因为它会被写入stdout_logfile的同一个文件中，
                                 默认为AUTO，即随便找个地方存，supervisord重启被清空，非必须设置。
;stderr_logfile_maxbytes=1MB
;stderr_logfile_backups=10
;stderr_capture_maxbytes=1MB   ; 和stdout_capture一样。默认为0，关闭状态。
;stderr_events_enabled=false   ; 默认为false
;environment=A="1",B="2"       ; 该子进程的环境变量，和别的子进程不共享。
;serverurl=AUTO

; The below sample eventlistener section shows all possible
; eventlistener subsection values, create one or more 'real'
; eventlistener: sections to be able to handle event notifications
; sent by supervisor.

;[eventlistener:theeventlistenername] ; 和program的地位一样，也是suopervisor启动的子进程，用来订阅supervisord发送的event。
                                        它的名字就叫listener，可以在listener里面做一系列处理，比如报警等等。
;command=/bin/eventlistener    ; 和上面的program一样，表示listener的可执行文件的路径。
;process_name=%(program_name)s ; 进程名。
;numprocs=1                    ; 相同的listener启动的个数。
;events=EVENT                  ; event事件的类型，只有写在这个地方的事件类型，才会被发送。


;buffer_size=10                ; 这个是event队列缓存大小，
                                 当buffer超过10的时候，最旧的event将会被清除，并把新的event放进去。
                                 默认值为10，非必须设置。
;directory=/tmp                ; 进程执行前，会切换到这个目录下执行
                                 默认为不切换，非必须设置。
;umask=022
;priority=-1                   ; 启动优先级，默认为-1。
;autostart=true                ; 是否在supervisord启动时一起启动，默认为true。
;autorestart=unexpected        ; 是否自动重启，和program中一样，分为true，false，unexpected等。
;startsecs=1                   ; 进程启动后跑几秒钟才被认定为成功启动，默认为1。
;startretries=3                ; 失败最大尝试次数，默认为3。
;exitcodes=0,2                 ; 期望的进程退出码。
;stopsignal=QUIT               ; 干掉进程的信号，默认为TERM，
                                 比如设置为QUIT，那么如果QUIT来干这个进程那么会被认为是正常维护，
                                 退出码也被认为是expected中的。
;stopwaitsecs=10
;stopasgroup=false
;killasgroup=false
;user=chrism                   ; 设置普通用户，可以用来管理该listener进程。
                                 默认为空，非必须设置。
;redirect_stderr=true          ; 为true的话，stderr的log会并入stdout的log里面，
                                 默认为false，非必须设置。
;stdout_logfile=/a/path
;stdout_logfile_maxbytes=1MB
;stdout_logfile_backups=10
;stdout_events_enabled=false   ; listener不能发送event。
;stderr_logfile=/a/path
;stderr_logfile_maxbytes=1MB
;stderr_logfile_backups
;stderr_events_enabled=false   ; listener不能发送event。
;environment=A="1",B="2"       ; 该子进程的环境变量。默认为空，非必须设置。
;serverurl=AUTO

; The below sample group section shows all possible group values,
; create one or more 'real' group: sections to create "heterogeneous"
; process groups.

;[group:thegroupname]  ; 给programs分组，划分到组里面的program不用一个一个去操作了，可以对组名进行统一的操作。
                         注意：program被划分到组里面之后，就相当于原来的配置从supervisor的配置文件里消失，
                         supervisor只会对组进行管理，而不再会对组里面的单个program进行管理。
;programs=progname1,progname2  ; 组成员，用逗号分开。
                                 必须设置。
;priority=999                  ; 相对于组和组之间的优先级。默认999，非必须设置。

; The [include] section can just contain the "files" setting.  This
; setting can list multiple files (separated by whitespace or
; newlines).  It can also contain wildcards.  The filenames are
; interpreted as relative to this file.  Included files *cannot*
; include files themselves.

;[include]                         ; 当要管理的进程很多时，写在一个文件里面有点大，
                                     可以把配置信息写到多个文件中，然后include进来。
;files = relative/directory/*.ini
```


# event

supervisor的event机制是一个监控/通知框架。

event是一串数据，分为header、body两部分。

* #### header

```bash
ver:3.0 server:supervisor serial:21 pool:listener poolserial:10 eventname:PROCESS_COMMUNICATION_STDOUT len:54
```

* ver：event协议的版本；
* server：supervisor的标识符，即[supervisord]块的identifier选项中的东西，默认为supervisor；
* serial：event的序列号，supervisord在运行过程中，发送的第一个event的序列号就是1，接下来的event依次类推；
* pool：listener的pool的名字，listener只启动一个进程的话，就没有pool的概念了，名字就是[eventlistener:theeventlistenername]；
* poolserial：serial是supervisord给每个event的编号，而poolserial是eventpool给发送到这个pool的event编的号；
* eventname：event的类型名称；
* len：表示header后面的body部分的长度。


* #### body

body的数据结构和event的具体类型相关，不同的event的类型，header结构都一样，但body的结构大多不一样。

PROCESS\_STATE\_EXITED

当supervisord管理的子进程退出时，supervisord就会产生PROCESS\_STATE\_EXITED这个event。

```bash
processname:cat groupname:cat from_state:RUNNING expected:0 pid:2766
```

processname：进程名字，是[program:x]配置的名字；
groupname：组名；
from_state：进程退出前的状态；
expected：默认情况下exitcodes是0和2，也就是说0和2是expected。其它的退出码就是unexpected；
pid：进程号。

listener和supervisord之间的通信过程
event的发起方是supervisord进程，接收方是listener。listener和program一样，都是supervisord的子进程，两者的在配置上很多选项也都一样。program，也就是我们要管理的进程，也可以发送event，进而和supervisord主动通信。

event协议

当supervisord启动时，如果listener配置为autostart=true，listener会作为supervisor的子进程被启动。listener启动后，会向自己的stdout写一个"READY"的消息，此时父进程supervisord读取到这条消息后，会认为listener处于就绪状态。listener处于就绪状态后，当supervisord产生的event在listener配置的可接受的events中时，supervisord会把该event发送给该listener。listener接收到event后，就可以根据event的header、body里的数据做一系列的处理了。处理完后，listener向自己的stdout写一个消息"RESULT\nOK"，supervisord接收到这条消息后。就知道listener处理event完毕了。


```python
# !/usr/bin/env python
# coding:utf-8
 
import sys
import os
import subprocess
# childutils这个模块是supervisor的一个模型，可以方便我们处理event消息。我们也可以自己按照协议，用任何语言来写listener，只不过用childutils更加简便罢了。
from supervisor import childutils
from optparse import OptionParser
import socket
import fcntl
import struct
 
__doc__ = "\033[32m%s,捕获PROCESS_STATE_EXITED事件类型,当异常退出时触发报警\033[0m" % sys.argv[0]
 
def write_stdout(s):
    sys.stdout.write(s)
    sys.stdout.flush()
# 定义异常
class CallError(Exception):
    def __init__(self,value):
        self.value = value
    def __str__(self):
        return repr(self.value)
# 定义处理event的类
class ProcessesMonitor():
    def __init__(self):
        self.stdin = sys.stdin
        self.stdout = sys.stdout
 
    def runforever(self):
        # 定义一个无限循环，可以循环处理event，
        # 也可以不用循环，把listener的autorestart配置为true，
        # 处理完一次event就让该listener退出，然后supervisord重启该listener，
        # 这样listener就可以处理新的event了。
        while 1:
            # 下面这个东西，向stdout发送"READY"，然后就阻塞在这里，一直等到有event发过来
            # headers，payload分别接收header和body的内容
            headers, payload = childutils.listener.wait(self.stdin, self.stdout)
            # 判断event是否是咱们需要的，
            # 不是的话，向stdout写入"RESULT\nOK"，并跳过当前循环的剩余部分
            if not headers['eventname'] == 'PROCESS_STATE_EXITED':
                childutils.listener.ok(self.stdout)
                continue
 
            pheaders, pdata = childutils.eventdata(payload+'\n')
            # 判读event是否是expected的，expected的话为1，否则为0
            # 这里的判断是过滤掉expected的event
            if int(pheaders['expected']):
                childutils.listener.ok(self.stdout)
                continue
 
            ip = self.get_ip('eth0')
            # 构造报警信息结构
            msg = "[Host:%s][Process:%s][pid:%s][exited unexpectedly fromstate:%s]" % (ip,pheaders['processname'],pheaders['pid'],pheaders['from_state'])
            # 调用报警接口
            subprocess.call("/usr/local/bin/alert.py -m '%s'" % msg,shell=True)
            # stdout写入"RESULT\nOK"，并进入下一次循环
            childutils.listener.ok(self.stdout)
 
    '''
    def check_user(self):
        userName = os.environ['USER']
        if userName != 'root':
            try:
                raise MyError('must be run by root!')
            except MyError as e:
                write_stderr( "Error occurred,value:%s\n" % e.value)
                sys.exit(255)
    '''
 
    def get_ip(self,ifname):
        s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        inet = fcntl.ioctl(s.fileno(), 0x8915, struct.pack('256s', ifname[:15]))
        ret = socket.inet_ntoa(inet[20:24])
        return ret

def main():
    parser = OptionParser()
    if len(sys.argv) == 2:
        if sys.argv[1] == '-h' or sys.argv[1] == '--help':
            print __doc__
            sys.exit(0)
    # (options, args) = parser.parse_args()
    # 下面表示只有supervisord才能调用该listener，否则退出
    if not 'SUPERVISOR_SERVER_URL' in os.environ:
        try:
            raise CallError("%s must be run as a supervisor event" % sys.argv[0])
        except CallError as e:
            write_stderr("Error occurred,value: %s\n" % e.value)
        return
 
    prog = ProcessesMonitor()
    prog.runforever()
 
if __name__ == '__main__':
    main()
```


# xml_rpc

supervisor提供两种管理方式：supervisorctl和web，它们其实都是通过xml_rpc来实现的。

> xml_rpc是使用http协议作为传输协议的rpc机制。

> RPC，Remote Procedure Call，远程过程调用，是一种通过网络在本地的机器上调用远端机器上服务的技术，这个过程也被大家称为“分布式计算”，是为了提高各个分立机器的“互操作性”而发明的技术。

一个rpc系统必然包括两部分：

1. rpc client，用来向rpc server调用方法，并接收方法的返回数据；
2. rpc server，用于响应rpc client的请求，执行方法，并回送方法执行结果。

在python里可以用SimpleXMLRPCServer和xmlrpclib两个模块分别实现服务端和客户端。

调用supervisor的xml_rpc接口：

```python
import xmlrpclib
p = xmlrpclib.Server('http://localhost:9001/RPC2')
# xmlrpclib.Server()里面的url和supervisor.conf里的配置是相关的
```

https://blog.csdn.net/LHWorldBlog/article/details/78518696

https://blog.csdn.net/shanliangliuxing/article/details/15499891

https://www.jianshu.com/p/3658c963d28b