信号
# 信号集设定
## sigset_t  set;
## int sigemptyset(sigset *set);//将某个信号集清空，成功返回0，失败返回-1
## int sigfillset(sigset *set);//将某个信号集置1，成功返回0，失败返回-1
## int sigaddset(sigset *set,int signum);//将某个信号加入信号集，成功返回0，失败返回-1
## int sigdelset(sigset *set,int signum);//将某个信号从信号集中删除；成功返回0，失败返回-1
## int sigismember(const sigset *set,int signum);//判断某个信号是否在信号集中，在返回1，不在返回0，错误返回-1；
## int sigprocmask(int how,const sigset *set,sigset *oldset);//成功返回0，失败返回-1
### how:SIG_BLOCK:set表示需要屏蔽的信号，mask|set;
###    :SIG_UNBLOCK:set表示需要解除屏蔽的信号,mask&~set；
###    :SIG_SETMASK:mask=set;
## int sigpending(sigst *set);//读取当前进程未决信号集

# 信号捕捉
## typedef void (*sighandler_t)(int);//函数指针
## sighandler_t signal(int signum,sighandler_t handler);//signum信号，handler调用的函数

## int sigaction(int signum,const struct sigaction *act,struct sigaction *oldact);//成功返回0，失败返回-1；
### struct sigaction{
###     void (*sa_handler)(int);
###     void (*sa_sigaction)(int,siginfo_t *,void*);
###     sigset_t sa_mask;
###     int sa_flags;
###     void (*sa_restorer)(void);
### }
### sa_restorer(弃用)
### sa_sigaction:当sa_falgs被设置为SA_SIGINFO标志时使用；
### sa_handler：指定信号捕捉后的处理函数名(即注册函数)。
### sa_mask: 调用信号处理函数时，所要屏蔽的信号集合(信号屏蔽字)。
### sa_flags：通常设置为0，表使用默认属性。

## 解决时序问题采用原子操作
## int sigsuspend(const sigset_t *mask);//挂起等待信号.
