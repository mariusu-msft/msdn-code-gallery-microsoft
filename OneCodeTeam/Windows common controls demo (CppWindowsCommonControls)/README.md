# Windows common controls demo (CppWindowsCommonControls)
## Requires
- Visual Studio 2008
## License
- Apache License, Version 2.0
## Technologies
- Windows UI
## Topics
- Common Controls
## Updated
- 05/05/2011
## Description

<p style="font-family:Courier New"></p>
<h2>WIN32 APPLICATION : CppWindowsCommonControls Project Overview</h2>
<p style="font-family:Courier New"></p>
<h3>Use:</h3>
<p style="font-family:Courier New"><br>
CppWindowsCommonControls contains simple examples of how to create common &nbsp;<br>
controls defined in comctl32.dll. The controls include Animation, ComboBoxEx, <br>
Updown, Header, MonthCal, DateTimePick, ListView, TreeView, Tab, Tooltip, IP <br>
Address, Statusbar, Progress Bar, Toolbar, Trackbar, and SysLink.<br>
<br>
</p>
<h3>Creation:</h3>
<p style="font-family:Courier New"><br>
First, build up the dialogs for use in this example according to the <br>
CppWindowsDialog example. Then link the application to comctl32.lib in the <br>
project's property page / Linker / Input / Additional Dependencies. Because <br>
the sample needs to work on Windows XP and Windows 2003 apart from Windows <br>
Vista, change the default target version to _WIN32_WINNT_WINXP in the <br>
targetver.h.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;#ifndef WINVER<br>
&nbsp;&nbsp;&nbsp;&nbsp;#define WINVER _WIN32_WINNT_WINXP&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// Originally 0x0600<br>
&nbsp;&nbsp;&nbsp;&nbsp;#endif<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;#ifndef _WIN32_WINNT<br>
&nbsp;&nbsp;&nbsp;&nbsp;#define _WIN32_WINNT _WIN32_WINNT_WINXP&nbsp;&nbsp;&nbsp;&nbsp;// Originally 0x0600<br>
&nbsp;&nbsp;&nbsp;&nbsp;#endif <br>
<br>
A. Animation Control<br>
<br>
Step1. Add the AVI resource IDR_UPLOAD_AVI according to the KB article:<br>
<br>
How to create a resource .dll file that contains an AVI file <br>
<a target="_blank" href="http://support.microsoft.com/kb/178199">http://support.microsoft.com/kb/178199</a><br>
<br>
Step2. In OnInitAnimationDialog, load and register animation control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_ANIMATE_CLASS;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step3. Create the animation control.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;RECT rc = { 20, 20, 280, 60 };<br>
&nbsp;&nbsp;&nbsp;&nbsp;HWND hAnimate = CreateWindowEx(0, ANIMATE_CLASS, 0, <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ACS_TIMER | ACS_AUTOPLAY | ACS_TRANSPARENT | WS_CHILD | WS_VISIBLE,
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rc.left, rc.top, rc.right, rc.bottom,
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hWnd, (HMENU)IDC_ANIMATION, hInst, 0);<br>
<br>
Step4. Open and play the AVI clip in the animation control.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;SendMessage(hAnimate, ACM_OPEN, (WPARAM)0, <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(LPARAM)MAKEINTRESOURCE(IDR_UPLOAD_AVI));<br>
&nbsp;&nbsp;&nbsp;&nbsp;SendMessage(hAnimate, ACM_PLAY, (WPARAM)-1, <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MAKELONG(/*from frame*/0, /*to frame*/-1));<br>
<br>
B. ComboBoxEx Control<br>
<br>
Step1. In OnInitComboBoxExDialog, load and register ComboBoxEx control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_USEREX_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create the ComboBoxEx control.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;RECT rc = { 20, 20, 280, 100 };<br>
&nbsp;&nbsp;&nbsp;&nbsp;HWND hComboEx = CreateWindowEx(0, WC_COMBOBOXEX, 0, <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CBS_DROPDOWN | WS_CHILD | WS_VISIBLE,
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rc.left, rc.top, rc.right, rc.bottom,
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hWnd, (HMENU)IDC_COMBOBOXEX, hInst, 0);<br>
<br>
Step3. Create an image list and associate the image list with the ComboBoxEx <br>
control. (ImageList_Create, CBEM_SETIMAGELIST)<br>
<br>
Step4. Add some items with image to the ComboBoxEx common control. <br>
(COMBOBOXEXITEM, CBEM_INSERTITEM)<br>
<br>
Step5. Destroy the image list on close. (ImageList_Destroy)<br>
<br>
C. Up-Down Control<br>
<br>
Step1. In OnInitUpdownDialog, load and register Updown control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_UPDOWN_CLASS;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create an Updown control and an Edit control. (CreateWindowEx)<br>
<br>
Step3. Attach the Updown control to its 'buddy' edit control. (UDM_SETBUDDY)<br>
<br>
D. Header Control<br>
<br>
Step1. In OnInitHeaderDialog, load and register Header control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_WIN95_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create an Header control. (CreateWindowEx)<br>
<br>
Step3. Resize the header control to fit the client rectangle. <br>
(HDM_LAYOUT, HDLAYOUT, SetWindowPos)<br>
<br>
Step4. Add Header items (HDITEM, HDM_INSERTITEM)<br>
<br>
Step5. In OnHeaderSize of the window, resize the Header control accordingly.<br>
(HDM_LAYOUT, HDLAYOUT, SetWindowPos)<br>
<br>
E. Month Calendar Control<br>
<br>
Step1. In OnInitMonthCalDialog, load and register MonthCal control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_DATE_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create a Month Calendar control. (CreateWindowEx)<br>
<br>
F. Date and Time Picker Control<br>
<br>
Step1. In OnInitDateTimePickDialog, load and register DateTimePick control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_DATE_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create a DateTimePick control. (CreateWindowEx)<br>
<br>
G. List View Control<br>
<br>
Step1. In OnInitListviewDialog, load and register Listview control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_LISTVIEW_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create a Listview control. (CreateWindowEx)<br>
<br>
Step3. Set up and attach image lists to list view common control. <br>
(ImageList_Create, ImageList_AddIcon, ListView_SetImageList)<br>
<br>
Step4. Add items to the the list view common control. <br>
(LVITEM, LVM_INSERTITEM)<br>
<br>
Step5. In OnListviewSize of the window, resize and re-arrange the Listview <br>
control to fit the client rectangle. (MoveWindow, LVM_ARRANGE)<br>
<br>
Step6. In OnListviewClose, free up the image list resources. <br>
(ImageList_Destroy)<br>
<br>
H. Tree View Control<br>
<br>
Step1. OnInitTreeviewDialog, load and register Treeview control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_TREEVIEW_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create a Treeview control. (CreateWindowEx)<br>
<br>
Step3. Set up and attach image lists to tree view common control. <br>
(ImageList_Create, ImageList_AddIcon, TreeView_SetImageList)<br>
<br>
Step4. Add items to the tree view common control. <br>
(TVITEM, TVINSERTSTRUCT, TVM_INSERTITEM)<br>
<br>
Step5. In OnTreeviewSize of the window, resize the Treeview control to fit <br>
the client rectangle. (MoveWindow)<br>
<br>
Step6. In OnTreeviewClose, free up the image list resources. <br>
(TreeView_GetImageList, ImageList_Destroy)<br>
<br>
I. Tab Control<br>
<br>
Step1. In OnInitTabControlDialog, load and register Tab control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_TAB_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create a Tab control. (CreateWindowEx)<br>
<br>
Step3. Add items to the tab common control. (TCITEM, TCM_INSERTITEM)<br>
<br>
Step4. In OnTabSize of the window, resize the Tab control to fit the client <br>
rectangle. (MoveWindow)<br>
<br>
J. Tooltip Control<br>
<br>
Step1. In OnInitTooltipDialog, load and register Tooltip control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_WIN95_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create a button control and a tooltip control. Note that a tooltip <br>
control should not have the WS_CHILD style, nor should it have an id, <br>
otherwise its behavior will be adversely affected, eg. tooltips displayed in <br>
wrong place or not at all. (CreateWindowEx)<br>
<br>
Step3. Associate the tooltip with the button control. (TOOLINFO, TTM_ADDTOOL)<br>
<br>
K. IP Address Control<br>
<br>
Step1. In OnInitIPAddressDialog, load and register IPAddress control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_INTERNET_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create the IPAddress control. (CreateWindowEx)<br>
<br>
L. Status Bar Control<br>
<br>
Step1. In OnInitStatusbarDialog, load and register StatusBar control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_BAR_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create the status bar control. (CreateWindowEx)<br>
<br>
Step3. Establish the number of partitions or 'parts' the status bar will <br>
have, their actual dimensions will be set in the parent window's WM_SIZE <br>
handler. (SB_SETPARTS)<br>
<br>
Step4. Put some texts into each part of the status bar and setup each part.<br>
(SB_SETTEXT)<br>
<br>
Step5. In OnStatusbarSize, partition the statusbar to keep the ratio of the <br>
sizes of its parts constant. Resize statusbar so it's always same width as <br>
parent's client area. (SB_SETPARTS, WM_SIZE)<br>
<br>
M. Progress Bar Control<br>
<br>
Step1. In OnInitProgressDialog, load and register Progress Bar control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_PROGRESS_CLASS;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create the progress bar control. (CreateWindowEx)<br>
<br>
Step3. Set the progress bar position. (PBM_SETPOS)<br>
<br>
N. Toolbar Control<br>
<br>
Step1. In OnInitToolbarDialog, load and register Toolbar control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_BAR_CLASSES;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create the toolbar control. (CreateWindowEx)<br>
<br>
Step3. Setup and add buttons to Toolbar. <br>
<br>
&nbsp;3.1 Send the TB_BUTTONSTRUCTSIZE to the toolbar control. If an application <br>
&nbsp;uses the CreateWindowEx function to create the toolbar, the application <br>
&nbsp;must send this message to the toolbar before sending the TB_ADDBITMAP or <br>
&nbsp;TB_ADDBUTTONS message. The CreateToolbarEx function automatically sends <br>
&nbsp;TB_BUTTONSTRUCTSIZE, and the size of the TBBUTTON structure is a parameter <br>
&nbsp;of the function.<br>
&nbsp;<br>
&nbsp;3.2 Add images (TBADDBITMAP, TB_ADDBITMAP)<br>
&nbsp;<br>
&nbsp;3.3 Add buttons (TBBUTTON, TB_ADDBUTTONS)<br>
&nbsp;<br>
Step4. Tell the toolbar to resize itself, and show it. (TB_AUTOSIZE)<br>
<br>
O. Trackbar control<br>
<br>
Step1. In OnInitTrackbarDialog, load and register Trackbar control class. <br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_WIN95_CLASSES; // Or ICC_PROGRESS_CLASS<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE;<br>
<br>
Step2. Create the Trackbar control. (CreateWindowEx)<br>
<br>
Step3. Set Trackbar range. (TBM_SETRANGE)<br>
<br>
P. SysLink Control<br>
<br>
Step1. In OnInitSysLinkDialog, load and register SysLink control class.<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;INITCOMMONCONTROLSEX iccx;<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwSize = sizeof(INITCOMMONCONTROLSEX);<br>
&nbsp;&nbsp;&nbsp;&nbsp;iccx.dwICC = ICC_LINK_CLASS;<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!InitCommonControlsEx(&iccx))<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return FALSE; <br>
<br>
Step2. Create the SysLink control. The SysLink control supports the anchor <br>
tag(&lt;a&gt;) along with the attributes HREF and ID. (CreateWindowEx) For example,<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;HWND hLink = CreateWindowEx(0, WC_LINK, <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_T(&quot;All-In-One Code Framework\n&quot;) \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_T(&quot;&lt;A HREF=\&quot;<a target="_blank" href="http://cfx.codeplex.com\&quot;&gt;Home&lt;/A&gt;">http://cfx.codeplex.com\&quot;&gt;Home&lt;/A&gt;</a> &quot;) \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_T(&quot;and &lt;A ID=\&quot;idBlog\&quot;&gt;Blog&lt;/A&gt;&quot;),
<br>
&nbsp; &nbsp; &nbsp; &nbsp;WS_VISIBLE | WS_CHILD | WS_TABSTOP, <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rc.left, rc.top, rc.right, rc.bottom,
<br>
&nbsp; &nbsp; &nbsp; &nbsp;hWnd, (HMENU)IDC_SYSLINK, hInst, NULL);<br>
<br>
Step3. In OnSysLinkNotify, capture the notifications associated with SysLink <br>
controls: NM_CLICK (syslink) and (for links that can be activated by the <br>
Enter key) NM_RETURN. If the link is a HREF, get its url from <br>
NMLINK.LITEM.szUrl, otherwise, get the ID from NMLINK.LITEM.szID.<br>
<br>
</p>
<h3>References:</h3>
<p style="font-family:Courier New"><br>
MSDN: About Window Classes <br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/ms633574.aspx">http://msdn.microsoft.com/en-us/library/ms633574.aspx</a><br>
<br>
Creating Common Controls<br>
<a target="_blank" href="http://winapi.foosyerdoos.org.uk/info/common_cntrls.php">http://winapi.foosyerdoos.org.uk/info/common_cntrls.php</a><br>
<br>
MSDN: Animation Control<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb761881.aspx">http://msdn.microsoft.com/en-us/library/bb761881.aspx</a><br>
<br>
MSDN: ComboBoxEx Control Reference<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb775740.aspx">http://msdn.microsoft.com/en-us/library/bb775740.aspx</a><br>
<br>
MSDN: Up-Down Control<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb759880.aspx">http://msdn.microsoft.com/en-us/library/bb759880.aspx</a><br>
<br>
MSDN: Header Control<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb775239.aspx">http://msdn.microsoft.com/en-us/library/bb775239.aspx</a><br>
<br>
MSDN: Month Calendar Control Reference<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760917.aspx">http://msdn.microsoft.com/en-us/library/bb760917.aspx</a><br>
<br>
MSDN: Date and Time Picker<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb761727.aspx">http://msdn.microsoft.com/en-us/library/bb761727.aspx</a><br>
<br>
MSDN: List View<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb774737.aspx">http://msdn.microsoft.com/en-us/library/bb774737.aspx</a><br>
<br>
MSDN: Tree View<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb759988.aspx">http://msdn.microsoft.com/en-us/library/bb759988.aspx</a><br>
<br>
MSDN: Tab<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760548.aspx">http://msdn.microsoft.com/en-us/library/bb760548.aspx</a><br>
<br>
MSDN: ToolTip<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760246.aspx">http://msdn.microsoft.com/en-us/library/bb760246.aspx</a><br>
<br>
MSDN: IP Address Control<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb761374.aspx">http://msdn.microsoft.com/en-us/library/bb761374.aspx</a><br>
<br>
MSDN: Status Bar<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760726.aspx">http://msdn.microsoft.com/en-us/library/bb760726.aspx</a><br>
<br>
MSDN: Progress Bar<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760818.aspx">http://msdn.microsoft.com/en-us/library/bb760818.aspx</a><br>
<br>
MSDN: Toolbar<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760435.aspx">http://msdn.microsoft.com/en-us/library/bb760435.aspx</a><br>
<br>
MSDN: Trackbar<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760145.aspx">http://msdn.microsoft.com/en-us/library/bb760145.aspx</a><br>
<br>
MSDN: SysLink<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb760704.aspx">http://msdn.microsoft.com/en-us/library/bb760704.aspx</a><br>
<br>
<br>
</p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img src="http://bit.ly/onecodelogo">
</a></div>
