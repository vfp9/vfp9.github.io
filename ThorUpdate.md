---
layout: page
permalink: /thorupdate/
---

## 支持 Thor 更新

以下步骤/说明允许在 Thor 更新对话框中包含你的项目，这样用户可以很容易的安装并更新你的项目到最新版本，而不用克隆你的项目库。 

1. 在你的项目中创建一个名为 ThorUpdater 的子目录；

2. 下载 [ThorUpdater.zip](https://vfpx.github.io/ThorUpdater/ThorUpdater.zip) 并将其解压至 ThorUpdater 目录。这个压缩文件包含文件 CreateThorUpdate.ps1、Project.txt、Version.txt、 Thor_Update_Template.prg 和 Thor_Update_Template_With_Menu.prg；

3. 编辑 Project.txt 来包含你的项目信息：

    - appName 是显示的项目名称
    
    - appID 类似于 appName，但是它是一个友好的 URL（没有空格和其他非法字符的 URL） 

    - majorVersion 是主版本号，例如 1.0

    - excludeFiles 是以逗号分隔的文件名列表，用于从压缩文件中排除一些文件。允许使用通配符，所以可以使用 *.bak 来排除备份文件。逗号前后不允许有空格，否则，将无法启作用。

    - excludeFolders 是以逗号分隔的目录名，用于从压缩文件中排除一些目录。在每个目录名的前后各加一个*号，因为它们被视为通配符（例如，*Docs*就表示排除目录名中包含 Docs 的目录）。逗号前后不允许有空格，否则，将无法启作用。

    注意： CreateThorUpdate.ps1 并不会查找 "appName =", "appID =", etc.；它仅检查“=”号后的内容，并按照内置的顺序依次得到项目名称、URL、版本等这些内容。

4. CreateThorUpdate.ps1使用PowerShell社区扩展（PSCX）中的一个库来压缩文件，所以要安装PSCX；见[https://github.com/Pscx/Pscx](https://github.com/Pscx/Pscx)的下载和说明。注意：如果你得到一个 "Install-Module不被识别为cmdlet、函数、脚本文件或可操作程序的名称 "的错误，你的PowerShell可能是一个旧版本；关于升级的细节，见[http://wahlnetwork.com/2015/12/21/how-to-upgrade-windows-powershell-to-version-5-0/](http://wahlnetwork.com/2015/12/21/how-to-upgrade-windows-powershell-to-version-5-0/)。

5. 因为它是被下载的，CreateThorUpdate.ps1 默认是被阻止的。右键单击它，选择 "属性"，打开 "解锁"，然后点击 "确定"。如果你没有看到按钮，它应该是好的。

    ![](/images/unblock.png)

6. 下面是关于 CreateThorUpdate.ps1 的一些细节，我们将在第 8 步运行它。它在 ThorUpdater 文件夹中生成一个名为 *appID*Version.txt 的 Thor 版本文件，其中 *appID* 是 Project.txt 中指定的 appID 值。CreateThorUpdate.ps1 在生成该文件时使用 Version.txt 作为模板。Thor 版本文件包含了指定当前版本的版本号的代码。Version.txt 使用 MajorVersion.JulianDate 来表示项目的版本号，其中MajorVersion 是 Project.txt 中指定的 majorVersion 值，JulianDate 是从 2001 年 1 月 1 日开始的当前日数。例如，对于 2017 年 10 月 12 日发布的新版本，JulianDate 的值是 6494。使用 JulianDate 的好处是，如果有必要，你可以从该值倒推，得到发布日期。Version.txt 是通用的；它使用 APPNAME 作为项目名称的占位符，使用 MAJORVERSION 作为 Thor 传入代码的更新对象的AvailableVersion 属性中的主要版本号的占位符。例如，如果Project.txt包含这个：

    ```
    appName = Project Explorer  
    appID = ProjectExplorer  
    majorVersion = 1.0
    ```

    那么如果在 2017 年 10 月 12 日运行，CreateThorUpdate.ps1 会在 ThorUpdater 文件夹中生成 ProjectExplorerVersion.txt，内容如下：

    ```fox
    lparameters toUpdateObject
    local ldDate, ;
    	lnJulian, ;
    	lcJulian
    ldDate   = date(2017,10,12)
    lnJulian = val(sys(11, ldDate)) - val(sys(11, {^2000-01-01}))
    lcJulian = padl(transform(lnJulian), 4, '0')
    toUpdateObject.AvailableVersion = 'Project Explorer-1.0.' + lcJulian + ;
    	'-update-' + dtoc(ldDate, 1)
    return toUpdateObject
    ```

    Version.txt 中 AvailableVersion 的格式--项目名称，一个破折号，版本号，一个破折号，一些文本（Thor似乎没有使用它），一个破折号，以及格式为 YYYMMDD 的发布日期--这是 Thor 的要求。
    
    如果你想使用一个不同的版本号系统，可以自由地编辑 Version.txt，使用你想要的任何机制来给 AvailableVersion 分配一个值。记住，这段代码是在用户的系统上执行的，而不是在你的系统上，所以你需要对这个值进行硬编码。

7. CreateThorUpdate.ps1在ThorUpdater文件夹中创建一个名为*appID*.zip的压缩文件，其中*appID*是Project.txt中指定的appID值。这个压缩文件包含了项目文件夹下所有子目录中的所有文件，但Project.txt的excludeFiles设置中指定的任何文件和excludeFolders设置中指定的任何文件夹除外。你可能希望Project.txt中至少有以下内容：

    ```fox
    excludeFiles = *.bak,*.fxp
    excludeFolders = *ThorUpdater*
    ```
    
8. 编辑完Project.txt后，你就可以创建Thor需要的文件来下载和安装或更新你的项目。右键单击ThorUpdater文件夹中的CreateThorUpdate.ps1，从快捷菜单中选择用PowerShell运行。

    注意：如果你收到脚本执行被禁止的信息，请点击Windows开始按钮，输入 "power"，然后选择Windows PowerShell来打开PowerShell命令窗口。键入：

        Set-executionpolicy remotesigned –scope currentuser

    然后执行CreateThorUpdate.ps1。
    
    CreateThorUpdate.ps1 创建 *appID*Version.txt 和 *appID*.zip。将这两个文件添加到你的版本库（如果你之前没有这样做），提交，并推送到远程版本库。每次发布新版本时，都要重复这个步骤。

9. 为了让 Thor 知道你的项目，你必须创建一个名为 Thor_Update_*appID*.prg 的 Thor 更新器程序。Thor_Update_Template.prg 和 Thor_Update_Template_With_Menu.prg 是你可以用于这样一个程序的模板（如果你想让你的工具出现在Thor的菜单中，请使用后者）；关于如何编辑以使其特定于你的项目，请参见相应 PRG 的注释。

10. 创建这个程序后，将其压缩并通过电子邮件发给 VFPX 的项目经理（projects@vfpx.org）。他们会把它添加到 Thor 仓库，这样 Thor 就知道你的项目了（管理员注意：下载/dl/thorupdate/Updater_PRGs/updates.zip，把 PRG 添加到 zip 中，然后重新上传文件）。这个步骤你只需要做一次。

11. 现在 Thor 知道了你的项目，下次用户在 VFP 的 Thor 菜单中选择检查更新时，Thor 会从你的资源库中下载 *appID*Version.txt，看到项目可以安装或新版本可以下载，并在更新对话框中显示给用户。如果用户选择安装项目或更新，Thor 会从你的资源库中下载 *appID*.zip 并在项目文件夹（Thor/Tools\Components\*appName*主文件夹的子目录）中解压，并在该文件夹中创建 *appID*VersionFile.txt，以便知道用户的版本，这样他们就不会被提示要更新，直到下一个版本。

12. 每次你发布一个新的版本，右键点击 ThorUpdater 文件夹中的 CreateThorUpdate.ps1，从快捷菜单中选择用 PowerShell 运行。这将创建 *appID*Version.txt 和 *appID*.zip。提交并推送到远程资源库。
