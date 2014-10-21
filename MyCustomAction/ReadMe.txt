
$Type=[BUTTON1]
$Target=[TARGETDIR]$IpValue=[EDITA1]$FanucPort=[EDITA2]$ShdrPort=[EDITA3]

	// Get user configuration for installation
	CConfigDlg dlg;
	INT_PTR res = dlg.DoModal();

	

	//contents=ReplaceOnce(contents,"IP=127.0.0.1", "IP=" + ipaddr);
	//contents=ReplaceOnce(contents,"Machine=DMG2796", "Machine=" + machinename);

// REmoved not necessary 
	status="Read MTCFanucAgent.ini";
	std::string contents; 
	ReadFile(path+"MTCFanucAgent.ini", contents);

	//FanucIpAddress=192.168.1.102
	ReplacePattern(contents, "FanucIpAddress=", "\n", "FanucIpAddress=" + ipaddr + "\n");
	//Protocol=LAN 
	if(type=="1")
		ReplacePattern(contents, "Protocol=", "\n", "Protocol=HSSB\n"); 
	else
		ReplacePattern(contents, "Protocol=", "\n", "Protocol=LAN\n"); 
		
	ReplacePattern(contents, "FanucPort=", "\n", "FanucPort=" + fanucPort +"\n"); 

	WriteFile(path+"MTCFanucAgent.ini",contents);

	status="Read agent.cfg";