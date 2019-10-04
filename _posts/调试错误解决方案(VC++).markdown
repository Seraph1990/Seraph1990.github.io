
文|Seraph
>这篇文章主要用来记录使用Visual Studio过程中，出现的各种error，并提供自己当时解决的方案。
但是，一个error可能由不用原因引起的，文中案例仅供大家参考。


1. nafxcwd.lib(thrdcore.obj) : error LNK2001: unresolved external symbol __endthreadex
解决：将工程设置为Using MFC in static library

2. cannot open file "mfc42u.lib"
解决：安装vc时没有安装Unicode版本（默认是不安装的），可以下载几个库文件copy到vc98/MFC/Lib，或者build选择非Unicode版本编译（也可以在Set Configuation中配置Unicode相关删除）

3. fatal error RC1107: invalid usage; use RC /? for Help
解决：查看vc++目录是否有问题
    <1>将附加额外目录暂时移至工程末尾
    <2>把其中的反斜线(/)替换为双反斜线(//)或者替换为斜线

4. LINK : fatal error LNK1000: Internal error during IncrBuildImage
解决：<1> 项目(Project)->属性(Property)->链接器(Linker)->常规(General) 下面的“启用增量链接(Enable Incremental Linking)”，将“是(/INCREMENTAL)”改为“否(/INCREMENTAL:NO)”。不过这又引入了另外一个警 告：FormatCom.obj : warning LNK4075: 忽略“/EDITANDCONTINUE”(由于“/INCREMENTAL:NO”规范)。
<2> 选择项目,属性(Property pages)->配置属性(Configuration Properties) ->C/C++，修改“调试信息格式(Debug Information Format)”为“程序数据库(Program Database(/Zi))”即可。

5. LINK1123:failure during conversion to COFF:file invalid or corrup
解决：将C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\bin\cvtres.exe目录下的cvtres.exe文件用C:\Windows\Microsoft.NET\Framework\v4.0.30319\cvtres.exe代替

6. error c2064:项不会计算为接受1个参数的函数   
解决：可能是运算符乘号未写

7. error c2228:"Grade"左边必须有类/结构/联合 
 解决：不一定是左边的类结构问题，前一语句缺少“；”也会导致这个错误。

8. error C2440: “=”: 无法从“const char [11]”转换为“LPCWSTR” 
解决：vc6.0运行没问题，vs2005之后默认Unicode字符集，可将其改为Muti-bye。

9. error LNK2019:无法解析的外部符号 _main，该符号在函数 ___tmainCRTStartup 中被引用 
解决：建错工程了，应该是win32 application(window应用程序） 
win32 application和win32 Console Application区别：
 win32 application就是普通的常见的窗口应用程序
 win32 Console Application就是MS-DOS窗口（命令提示符）

10. error C4996:'sprintf':This fuction or variable may be unsafe 
解决：将‘sprintf’改为‘sprintf_s’，警告就不会再有了。
很多函数不进行参数检测（越界类等...),微软担心使用这些会造成内存异常，所以就改写了同样的功能的函数，改写的函数进行了参数的检测，使用这些新的函数会更安全和便捷。一般只需加_s就行。

11. error C2084: 函数“XXXXXX“已有主体 
解决：检查是否有重名的函数定义

12. error C2065:'hInstance，NULL' : undeclared identifier  
解决：主要是“，”是中文字符照成的，可能还会报warning C4003: not enough actual parameters for macro 'CreateWindowA'错

13. 致命错误 RC1015: 无法打开包含文件 'afxres.h' 
解决：实际上这个问题很多情况下是由于路径设置的问题引起的
**executatble files:**C:\Program Files\Microsoft Visual Studio\Common\MSDev98\BinC:\Program Files\Microsoft Visual Studio\VC98\BINC:\Program Files\Microsoft Visual Studio\Common\TOOLSC:\Program Files\Microsoft Visual Studio\Common\TOOLS\WINNT
**include files:**C:\Program Files\Microsoft Visual Studio\VC98\INCLUDEC:\Program Files\Microsoft Visual Studio\VC98\MFC\INCLUDEC:\Program Files\Microsoft Visual Studio\VC98\ATL\INCLUDE
**library files:**C:\Program Files\Microsoft Visual Studio\VC98\LIBC:\Program Files\Microsoft Visual Studio\VC98\MFC\LIB
**source files:**C:\Program Files\Microsoft Visual Studio\VC98\MFC\SRCC:\Program Files\Microsoft Visual Studio\VC98\MFC\INCLUDEC:\Program Files\Microsoft Visual Studio\VC98\ATL\INCLUDEC:\Program Files\Microsoft Visual Studio\VC98\CRT\SRC

14. error C2065: ‘xxxxxxxx’：undeclared identifier
解决：很多是因为“；”或者其他符号是中文下输入，造成的。

15. error C2653:  is not a class or namespace name 
解决：没建立一个新类都要在.cpp文件中加入#include "stdafx.h",而且要加在第一行,
编译器通过一个头文件stdafx.h 来使用预编译头文件。

16. 缺失return经常会使弹出内存操作错误 
解决：理清程序结构，找到漏写的返回值。

17. First-chance exception in main.exe: 0xC0000005: Access Violation. 
解决：访问违例，使用空间，但是未申请，也可能在使用之前被delete了。

18. LINK : fatal error LNK1168: cannot open Debug/ling.exe for writing  
解决：结束ling.exe进程。

19. error LNK2001: 无法解析的外部符号 "public: void __thiscall CSketcherView::OnColorBlack  
解决：OnColorBlack在源文件中未写

20. 菜单响应函数消息类型不见了！
 解决：直接删除.ncb文件

21. error LNK2019 : unresolved external symbol __imp__PlaySoundW@12 referenced in function _WinMain@16  
解决：#pragma comment(lib,"winmm.lib")

22.  please enter the path for mfcs42d.pdb    
解决：将debug文件夹内容全部删除

23. 调试错误 ASSERTE(_CrtIsValidHeapPointer(pUserData))
 解决：delete 野指针前给指针赋空

24. 无法启动此程序 ，因为计算机中丢失MFC80UD.DLL 
解决：把工程debug下文件全部删除，然后rebulid project

25. VC6.0 error LNK2001: unresolved external symbol _main   
解决：[Project] --> [Settings] --> 选择"Link"属性页, 在Project Options中将/subsystem:console改成/subsystem:windows

26. fatal error RC1004: unexpected end of file found        
解决： 头文件里少了结尾的回车

27. vc助手写到一般时突然没有提示了  
解决：可能是前面有哪句写错了，然后导致后面识别的全是字符

28.  File f:/dd/vctools/vc7libs/ship/atlmfc/src/mfc/viewscrl.cpp, Line 385
解决：需要在类开时时,增加SetScrollSizes ( MM_TEXT,CSize (0 , 0 ) );

29. error C2668: 'sqrt' : ambiguous call to overloaded function   
解决：sqrt处理类型必须是double

30. error C2144:syntax error : 'char' should be preceded by ';'  
解决：如果在 a.h 里缺少分号, 则编译器会在 b.h 中会提示错误. 所以要在 a.h 中找错误

31. <dshow.h>无法打开
解决：vs编译器没有包含dx的drawshow中的include、lib

32. fatal error C1001: An internal error has occurred in the compiler. 
解决：清理解决方案，然后build

33. 源文件与模块生成时的文件不同
解决：清空解决方案，重新生成解决方案

34. error LNK2001: 无法解析的外部符号 "public: virtual void __thiscall CDib::GetTmplPos(void)" (?GetTmplPos@CDib@@UAEXXZ)  
解决：虚函数格式错误，必须在源文件函数后加｛｝

35. x.exe中的0x77dd15de处有未经处理的异常:0xC015000F:正被停用的激活上下文不是最近激活的      
解决：在Visual Studio中，选择Debug | Exceptions菜单项，在弹出的对话框中，勾选所有的Win32 Exceptions。这样就有机会在第一时间（异常处理前）看到自己的代码中发生了什么错误而导致抛出异常，从而改正错误，消除程序中的隐患。
（注：可能是析构函数中释放并未初始化的变量）

36. 在VC++6.0中出现failed to (or don't know how to) build 'D:\VC98\MFC\SRC\APPMODUL.CPP'
解决：系统目录设置问题：找到××.dsp文件（××为工程名），用记事本打开，找到如下：SOURCE="D:\Program Files\Microsoft Visual Studio\VC98\MFC\SRC\APPMODUL.CPP"    # End Source File    # Begin Source File对SOURCE修改。

37. error C2146: syntax error : missing ';' before identifier 'PVOID64'
解决：将VS编译器环境中directdraw包含文件和包含库调至默认库下方.
 vs中会先加载项目属性中的包含文件和库，再加载vs本身配置的属性。
 所以，导致有些对库包含顺序有要求的库文件出错。——也就是说，directdraw不能在项目属性中设置

38. LINK :fatal error LNK1123: failure during conversion to COFF: file invalid or corrupt    
 解决：项目-->工程属性->配置属性-> 清单工具->输入和输出->嵌入清单，选择[否]

39. fatal error C1033: cannot open program database 'e:\实验室工程\newassistivev    
解决：将文件夹换成可读写状态

40. fatal error C1001: An internal error has occurred in the compiler.
解决：将解决方案清理，再重建（因为解决方案不是最新的）

41. 弹出不能找到“SpeechRecognizeBase.h”等文件
解决：将项目属性的链接和附加目录修改好

42. fatal error C1083:NO such file or directory
解决：项目属性附加目录添加：$(ProjectDir)，表示当前工程目录

43. 显示未声明某变量
解决：确认是否有，如果其在另一关联文件定义了，注意要用extern声明该变量。

44. 断点无效
解决：1）清空生成的解决方案，重新生成
2）将工具->选项->调试里->常规 找到  要求原文件与原始版本完全匹配 不要打勾
（此方法最后试用）

45. vc80.pdb
解决：将文件路径全部改成英文

46. error C2143: syntax error : missing ';' before '<'
error C2433: 'CDib:: vector' : 'virtual' not permitted on data declarations 
error C4430: missing type specifier - int assumed. Note: C++ does not support default-int
error C2238: unexpected token(s) preceding ';'
解决：使用vector，未写using namespace std;

47. LINK : fatal error LNK1104: 无法打开文件“ejTTS.lib”
解决：将链接器中的附加库目录修改为正确的路径

48. chkstk.asm 错误
解决：在项目-》属性-》配置属性-》链接器-》系统，将堆栈保留大小弄大点，如50M（52428800）是堆太小加载溢出（如数组buffer定义的太大就会造成此现象）

49. error C2065: 'IDD_DIALOG_WNDSIZE': undeclared identifier
解决：将resources.h包含到该对话框头文件中来

50. 当编译后，按F5进行调试，断点无效（或有效，但是位置乱跳）
解决：勾选 工具-》调试-》常规 要求源文件与原始版本完全匹配

51. 程序通过VS编译器F5运行可以，直接点击exe运行不正常
解决：写绝对路径，问题就会消失。
缺省情况下：调试时使用的工作目录是你的项目所在的目录。而直接运行时，是你的可执行文件所在的目录。
（有则有，无则无，不会无中生有，定是另有乾坤）

52. 加入某些资源文件在最终程序中是有效果的，但是又用vs搜寻其ID不到
解决：清理解决方案，重新生成解决方案

53. cannot convert parameter 1 from 'const char *' to 'LPCWSTR' 
解决：将字符串用_T()转换或修改字符集为多字节字符集（vs05默认为UNICODE）
注：_T()包含在tchar头文件里

54. error C4430: missing type specifier - int assumed. Note: C++ does not
解决：给函数声明加上返回类型
注：vc6.0默认类型为int型，而vs不会这么做，所以会报错。

55. 放在桌面（win8）的工程文件无法生成动态链接库DLL
解决：将工程移置其他目录尝试
（未知根源，关闭工程时还会报无法保存项目设置信息）

56. 生成的dll无法起到效果
解决：注意系统有分64和32，64位程序必须调用64的dll
（用相应的平台生成dll文件）

57. warning C4786: std::reverse_iterator<std::basic_string<char,std::char_traits<char>,std::allocator<char> > const *,std::basic_string<char,std::char_traits<char>,std::allocator<char> >,std::basic_string<char,std:: char_traits<char>,std::allocator<char> > const &,std::basi。。。
解决：在#include <vector>前加上  #pragma warning(disable:4786)，强制去除警告
注：vc6.0对vector支持不是很好，所以才会出现此警告。

58. please enter the path for mfcs42d.pdb 提示解决方法
解决：Project settings | Link | Debug, 不选 "Separate types"。然后，rebuild all。重新把Separate types 勾选上。

59.LINK : fatal error LNK1104: 无法打开文件“Log.lib xxx.lib xxx.lib”
解决：VS10库包含之间是用“；”隔离开来的，VC6.0是用空格。

60. R6010 abort() has been called
解决：一般是指针访问越界导致的，仔细检查是否有内存写入失败，依然会当作成功取获取指针，并读取未写入任何信息的内存控件。

61. error LNK2019: unresolved external symbol _main referenced in function ___tmainCRTStartup
解决：将“Configuration”-“General”中Configuration Type修改为Dynamic Library(.dll)
原因：由于自己是要编译DLL工程，没有相应的启动入口函数。

62. error C4996: 'fopen': This function or variable may be unsafe. Consider using fopen_s instead.
解决：在预处理器定义中添加``_CRT_SECURE_NO_WARNINGS``
或者新建工程时不勾选：安全开发生命周期(SDL)检查
原因：因为很多版本都没有使用安全函数，为减少改动，关闭相关检查。

62. `new xxx`一个自建类时，弹错：`应输入类型说明符`。
解决：这种情况基本时函数或变量名与``new``的那个类同名造成的，将函数同名函数或者同名变量名修改下就可以了。
解析：编辑器不是万能的，我们不能自以为编译器可以处理什么，而是要了解编译器处理逻辑，并知道哪些时编译器处理不了的。这个时候就很体现平常良好的编程习惯的好处了，我们一般变量名会全部小写，类首字母大写，这样就完全不会出现变量名和类名重名的情况。

63. VC转VS工程出现：LINK : fatal error LNK1117: 选项“mapinfo:lines”中的语法错误。
解决：`配置属性-链接器-命令行`右侧的附加选项删除`mapinfo:lines`。

64. error LNK2019: 无法解析的外部符号 _GetIfEntry@4 ，
解决：缺失链接库，添加`#pragma comment(lib, "IPHlpApi.lib")`。

65.  使用CArray数组，报 afxtempl.h Line:254错误。
解决：可能是数组越界导致。不一定是指CArray本身，程序任何地方数组越界，都可能不可预知的错误。

66. 



>每一天都是一个新的日子。走运当然是好的，不过我情愿做到分毫不差。这样，运气来的时候，你就有所准备了。------《老人与海》
