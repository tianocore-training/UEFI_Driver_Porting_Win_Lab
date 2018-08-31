---?image=assets/images/gitpitch-audience.jpg
@title[UEFI_Driver_Porting Lab]
<br><br><br><br><br>
## <span class="gold"   >UEFI & EDK II Training</span>

#### How to Write a UEFI Driver Lab - Windows

<br>
<span style="font-size:0.75em" ><a href='http://www.tianocore.org'>tianocore.org</a></span>
Note:
  PITCHME.md for UEFI / EDK II Training  UEFI Driver Porting Lab - Windows

  Copyright (c) 2018, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.



---  
@title[Lesson Objective]
<BR>
### <p align="center"<span class="gold"   >Lesson Objective </span></p><br>

<!---  Add bullets using https://fontawesome.com/cheatsheet certificate
-->
<ul style="list-style-type:none">
 <li>@fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Compile a UEFI driver template created from<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; UEFI Driver Wizard</span> </li><br>
 <li>@fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Test driver w/ Nt32 emulation using UEFI Shell 2.0</span></li><br>
 <li>@fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Port code into the template driver</span> </li>
</ul>

---?image=assets/images/binary-strings-black2.jpg
@title[UEFI Driver Lab]
<br><br><br><br><br><br><br>
### <span class="gold"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UEFI Driver Porting Lab </span>
<span style="font-size:0.9em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This Lab uses the template UEFI driver created by the<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; UEFI Driver Wizard</span>


---?image=/assets/images/slides/Slide_LabSec.JPG
@title[Lab 2: Building a UEFI Driver]
<br>
<br>
<p align="Left"><span class="gold" >Lab 2: Building a UEFI Driver</span></p>
<br>
<div class="left1">
<span style="font-size:0.8em" >In this lab, you’ll build a UEFI Driver created by the UEFI Driver Wizard.<br>
You will include the driver in the Nt32 project. <br>Build the UEFI Driver from the Driver Wizard </span>
</div>
<div class="right1">
<span style="font-size:0.8em" >&nbsp;  </span>
</div>

---?image=/assets/images/slides/Slide5.JPG
@title[Compile a UEFI Driver?]
<p align="right"><span class="gold" >Compile a UEFI Driver</span></p>

Note:
|Standalone |In a Project	|
|-----------|--------------|
|The build command directly compiles the .INF file |Include the .INF file in the project’s .DSC file	|
|Results:  The driver’s  .EFI file is located in the Build directory|	Results:  The driver’s .EFI file is a part of the project in the Build directory|

---
@title[Lab2: Build the UEFI Driver?]
<p align="right"><span class="gold" >Lab 2: Build the UEFI Driver</span></p>
<br>
<ul>
   <li><span style="font-size:0.8em" >Perform <a href="https://gitpitch.com/Laurie0131/Platform_Build_Win_Lab/master#/9">Lab Setup</a> from previous Nt32Pkg Labs  </span></li>
   <li><span style="font-size:0.8em" >Open `C:/FW/edk2/Nt32Pkg/Nt32Pkg.dsc`</span></li>
   <li><span style="font-size:0.8em" >Add the following to the `[Components]` section: </span><br><span style="font-size:0.6em" >*Hint:*add to the last module in the `[Components]` section   </span></li>
<pre lang="php">
```
    # Add new modules here
   MyWizardDriver/MyWizardDriver.inf
```
</pre>
   <li><span style="font-size:0.8em" >Save and close the file `C:/FW/edk2/Nt32Pkg/Nt32Pkg.dsc`  </span></li>
</ul>



---
@title[Lab 2 Build and Test Driver]
<p align="right"><span class="gold" >Lab 2: Build and Test Driver</span></p>
<span style="font-size:0.8em" >Open a VS  Command Prompt and type: `cd C:/FW/edk2` then </span>
```
C:/FW/edk2> edksetup
```
<p style="line-height:80%"><span style="font-size:0.8em" > Build `MyWizardDriver` </span></p>

```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run
```

<p style="line-height:80%"><span style="font-size:0.7em" >Load the UEFI Driver from the shell
<br>&nbsp;&nbsp;&nbsp; At the Shell prompt, type &nbsp;<span style="background-color: #101010"><font color="yellow">`Shell> `</font>`fs0:`</span>
<br>&nbsp;&nbsp;&nbsp; Type:&nbsp; <span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`</span></span></p>
<p style="line-height:80%"><span style="font-size:0.6em" ><b>Build ERRORS:</b> Copy the solution files from `~/FW/LabSampleCode/LabSolutions/LessonC.1` to `C:/FW/edk2/MyWizardDriver`	</span></p>


Note: 
continue to next slide


---?image=/assets/images/slides/Slide8.JPG
@title[Lab 2 Test Driver Drivers]
<p align="right"><span class="gold" >Lab 2: Test Driver</span></p>
<br>
<span style="font-size:0.8em" >At the shell prompt Type: <span style="background-color: #101010">`drivers`</span></span><br>
<span style="font-size:0.7em" >Verify the UEFI Shell loaded the new driver. 
The `drivers` command will display the driver information and a driver handle number ("a9" in the example screenshot )</span>


Note:

Same as slide



---?image=/assets/images/slides/Slide9.JPG
@title[Lab 2 Test Driver -Dh]
<p align="right"><span class="gold" >Lab 2: Test Driver</span></p>
<br>
<span style="font-size:0.8em" >At the shell prompt using the handle from the `drivers` command, Type:&nbsp; <span style="background-color: #101010">`dh -d a9`</span></span>

<div class="left">
<span style="font-size:0.6em" ><i>Note:</i>  The value `a9` is the driver handle for MyWizardDriver.  The handle value may change based on your system configuration.(see example screenshot - right)</span>

</div>
<div class="right">
<span style="font-size:0.8em" ></span>
</div>

Note:

Same as slide




---?image=/assets/images/slides/Slide10.JPG
@title[Lab 2 Test Driver -unload]
<p align="right"><span class="gold" >Lab 2: Test Driver</span></p>
<br>
<span style="font-size:0.8em" >At the shell prompt using the handle from the `drivers` command, Type:&nbsp; <span style="background-color: #101010">`unload a9`</span></span>

<div class="left1">
<span style="font-size:0.7em" >See example screenshot - right</span><br>
<span style="font-size:0.7em" >Type:&nbsp; <span style="background-color: #101010">`drivers`</span> again</span><br><br>
<span style="font-size:0.7em" >Notice results of `unload` command</span><br><br>
<span style="font-size:0.7em" >Exit, type <font color="yellow">`FS0:/ >`</font> `Reset`</span><br>
</div>
<div class="right1">
<span style="font-size:0.8em" ></span>
</div>

Note:


END of Lab 2


---?image=/assets/images/slides/Slide_LabSec.JPG
@title[Lab 3: Component Name Section]
<br>
<br>
<p align="Left"><span class="gold" >Lab 3: Component Name</span></p>
<br>
<div class="left1">
<span style="font-size:0.8em" >In this lab, you’ll change the information reported to the drivers command using the ComponentName and ComponentName2 protocols.</span>
</div>
<div class="right1">
<span style="font-size:0.8em" >&nbsp;  </span>
</div>

---
@title[Lab 3: Component Name ]
<p align="right"><span class="gold" >Lab 3: Component Name</span></p>
<br>
<ul>
   <li><span style="font-size:0.8em" ><b>Open</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > `C:/FW/edk2/MyWizardDriver/ComponentName.c`</span></li>
   <li><span style="font-size:0.8em" ><b>Change</b>&nbsp;&nbsp; the string returned by the driver from `MyWizardDriver` to: &nbsp;&nbsp;&nbsp; <span style="background-color: #101010"><font color="#a8ff60">`UEFI Sample Driver`</font></span></span></li>
<pre lang="c">
```
  /// Table of driver names
 ///
 GLOBAL_REMOVE_IF_UNREFERENCED 
 EFI_UNICODE_STRING_TABLE mMyWizardDriverDriverNameTable[] = {
   { "eng;en", (CHAR16 *)L"UEFI Sample Driver" },
   { NULL, NULL }
 };
```
</pre>
   <li><span style="font-size:0.8em" ><b>Save</b> and close the file: </span><span style="font-size:0.7em" >`C:/FW/edk2/MyWizardDriver/ComponentName.c`  </span></li>
</ul>


---?image=/assets/images/slides/Slide13.JPG
@title[Lab 3 Build and Test Driver]
<p align="right"><span class="gold" >Lab 3: Build and Test Driver</span></p>
<br>
<p style="line-height:80%"><span style="font-size:0.8em" > Build the MyWizardDriver </span></p>

```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run
```

<p style="line-height:80%"><span style="font-size:0.7em" >Load the UEFI Driver from the shell
<br>&nbsp;&nbsp;&nbsp; At the Shell prompt, type &nbsp;<span style="background-color: #101010"><font color="yellow">`Shell> `</font>`fs0:`</span>
<br>&nbsp;&nbsp;&nbsp; Type:&nbsp; <span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`</span></span></p>

<div class="left">
<span style="font-size:0.7em" >Type:&nbsp; <span style="background-color: #101010">`drivers`</span></span><br>
<span style="font-size:0.7em" >Observe the change in the string that the driver returned </span><br>
<br>
<span style="font-size:0.7em" >Exit, type <font color="yellow">`FS0:/ >`</font> `Reset`</span><br>
</div>
<div class="right">
<span style="font-size:0.8em" ></span>
</div>

Note: 
Lab 3 finished


---?image=/assets/images/slides/Slide_LabSec.JPG
@title[Lab 4: Port Supported Section]
<br>
<br>
<p align="Left"><span class="gold" >Lab 4: Porting the Supported & Start Functions</span></p>
<br>
<div class="left1">
<span style="font-size:0.8em" >The UEFI Driver Wizard produced a starting point for driver porting … so now what?<br><br>In this lab, you’ll port the “Supported” and “Start” functions for the UEFI driver</span>
</div>
<div class="right1">
<span style="font-size:0.8em" >&nbsp;  </span>
</div>



---?image=/assets/images/slides/Slide15.JPG
@title[Lab 4: Port Supported-Start]
<p align="center"><span class="gold" >Lab 4: Porting Supported and Start</span></p>
<span style="font-size:01.1em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>Review the Driver Binding Protocol</b></span>

Note:

- Port Supported() to check for a specific protocol before returning ‘Success’
- Port Start() to allocate a memory buffer and fill it with a specific value

---
@title[Lab 4: Supported Port]
<p align="right"><span class="gold" >Lab 4: The `Supported()` Port</span></p>
<p style="line-height:80%"><span style="font-size:0.8em" >The UEFI Driver Wizard produced a `Supported()` function but it only returns `EFI_UNSUPPORTED` </span></p>
<span style="font-size:0.9em" ><Font color="yellow"><b>Supported Goals: </b></font> </span></li>
<ul style="list-style-type:disc">
  <li><span style="font-size:0.8em" >Checks if the driver supports the device for the specified controller handle </span></li>
  <li><span style="font-size:0.8em" >Associates the driver with the Serial I/O protocol </span></li>
  <li><span style="font-size:0.8em" >Helps locate a protocol’s specific GUID through  UEFI Boot Services’ function </span></li>
</ul>

Note: 

Same as slide


---?image=/assets/images/slides/Slide17.JPG
@title[Lab 4: Help from Robust Libraries]
<p align="right"><span class="gold" >Lab 4: Help from Robust Libraries</span></p>
<span style="font-size:0.8em" >EDK II has libraries to help with porting UEFI Drivers </span><br>
<ul style="list-style-type:none">
  <li>@fa[book gp-bullet-gold]<span style="font-size:0.75em" >&nbsp;&nbsp;`AllocateZeroPool()` include - `[MemoryAllocationLib.h]`  </span></li><br>
  <li>@fa[book gp-bullet-gold]<span style="font-size:0.75em" >&nbsp;&nbsp;`SetMem16()`   include - `[BaseMemoryLib.h]`  </span></li>
</ul>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<span style="font-size:0.6em" >Check the MdePkg with libraries help file (.chm format) </span><br>


Note: 

---
@title[Lab 4: Update Supported ]
<p align="right"><span class="gold" >Lab 4: Update Supported </span></p>
<br>
<ul>
   <li><span style="font-size:0.8em" ><b>Open</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > `C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`</span></li>
   <li><span style="font-size:0.8em" ><b>Locate</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > ` MyWizardDriverDriverBindingSupported()`, 
       the supported function for this driver and comment out the "`//`" in the line: <span style="background-color: #101010">"`return EFI_UNSUPPORTED;` "</span> </span></li>
<pre lang="c">
```
EFI_STATUS
EFIAPI
MyWizardDriverDriverBindingSupported (
  IN EFI_DRIVER_BINDING_PROTOCOL  *This,
  IN EFI_HANDLE                   ControllerHandle,
  IN EFI_DEVICE_PATH_PROTOCOL     *RemainingDevicePath OPTIONAL
  )
{
  // return EFI_UNSUPPORTED;
}
```
</pre>
   <li><span style="font-size:0.8em" > <b>copy</b> and past (next slide)</span></li>
</ul>

Note: 

This code checks for a specific protocol before returning a status for the supported function (EFI_SUCCESS if the protocol GUID exists).


---
@title[Lab 4: Update Supported 02 ]
<p align="right"><span class="gold" >Lab 4: Update Supported Add Code </span></p>
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > the following code for the supported function ` MyWizardDriverDriverBindingSupported()`:</span></p>
```C
  EFI_STATUS Status;
  EFI_SERIAL_IO_PROTOCOL *SerialIo;
  Status = gBS->OpenProtocol (
                  ControllerHandle,
                  &gEfiSerialIoProtocolGuid,
                  (VOID **) &SerialIo,
                  This->DriverBindingHandle,
                  ControllerHandle,
                  EFI_OPEN_PROTOCOL_BY_DRIVER | EFI_OPEN_PROTOCOL_EXCLUSIVE
                  );

  if (EFI_ERROR (Status)) {
	 return Status; // Bail out if OpenProtocol returns an error
  }

    // We're here because OpenProtocol was a success, so clean up
     gBS->CloseProtocol (
        ControllerHandle,
        &gEfiSerialIoProtocolGuid,
        This->DriverBindingHandle,
        ControllerHandle
        );
  	
     return EFI_SUCCESS; 
```


---
@title[Lab 4: Notice UEFI Driver Wizard Includes  ]
<p align="right"><span class="gold" >Lab 4: Notice UEFI Driver Wizard Includes</span></p>
<ul style="line-height:0.8;">
   <li><span style="font-size:0.8em" ><b>Open</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > `C:/FW/edk2/MyWizardDriver/MyWizardDriver.h`</span></li>
   <li><span style="font-size:0.8em" ><b>Notice</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > the following include statement is already added by the driver wizard: </span></li>
<pre lang="c">
```
// Produced Protocols
//
#include <Protocol/SerialIo.h>
```
</pre>
   <li><span style="font-size:0.8em" ><b>Review</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > the Libraries section and see that UEFI Driver Wizard automatically includes library headers based on the form information. Also other common libary headers were included </span></li>
<pre lang="c">
```
// Libraries
//
#include <Library/UefiBootServicesTableLib.h>
#include <Library/MemoryAllocationLib.h>
#include <Library/BaseMemoryLib.h>
#include <Library/BaseLib.h>
#include <Library/UefiLib.h>
#include <Library/DevicePathLib.h>
#include <Library/DebugLib.h>
```
</pre>
</ul>

Note: 


---
@title[Lab 4: Update the Start  ]
<p align="right"><span class="gold" >Lab 4: Update the `Start()` </span></p>
<ul style="line-height:0.8;">
   <li><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > the following in  `MyWizardDriver.c` after the <br><span style="background-color: #101010">`#include “MyWizardDriver.h”` </span>line: </span></li>
<pre lang="c">
```
#define  DUMMY_SIZE 100*16		// Dummy buffer
CHAR16	*DummyBufferfromStart = NULL;
```
</pre>
    <li><span style="font-size:0.8em" ><b>Locate</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > ` MyWizardDriverDriverBindingStart()`,  the start function for this driver and comment out the "`//`" in the line <span style="background-color: #101010">"`return EFI_UNSUPPORTED;` "</span></span></li>
<pre lang="c">
```
EFI_STATUS
EFIAPI
MyWizardDriverDriverBindingStart (
  IN EFI_DRIVER_BINDING_PROTOCOL  *This,
  IN EFI_HANDLE                   ControllerHandle,
  IN EFI_DEVICE_PATH_PROTOCOL     *RemainingDevicePath OPTIONAL
  )
{
  // return EFI_UNSUPPORTED;
}
```
</pre>
   
</ul>

Note: 


---
@title[Lab 4: Update Start 02 ]
<p align="right"><span class="gold" >Lab 4: Update Start Add Code </span></p>
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the following code for the start function ` MyWizardDriverDriverBindingStart()`:</span></p>
```C
	if (DummyBufferfromStart == NULL) {     // was buffer already allocated?
		DummyBufferfromStart = (CHAR16*)AllocateZeroPool (DUMMY_SIZE * sizeof(CHAR16));
	}

	if (DummyBufferfromStart == NULL) {
		return EFI_OUT_OF_RESOURCES;    // Exit if the buffer isn’t there
	}

	SetMem16 (DummyBufferfromStart, (DUMMY_SIZE * sizeof(CHAR16)), 0x0042);  // Fill buffer

	return EFI_SUCCESS;
```
<ul style="list-style-type:disc">
 <li><span style="font-size:0.65em" >Notice the Library calls to `AllocateZeroPool()` and `SetMem16()`</span></li>
 <li><span style="font-size:0.65em" >The `Start()` function is where there would be calls to "`gBS->InstallMultipleProtocolInterfaces()`"</span></li>
</ul>


Note:

- This code checks for an allocated memory buffer. If the buffer doesn’t exist, memory will be allocated and filled with an initial value (0x0042). 
- this lab's start does **not** do anything useful but if it did it would make calls to gBS->InstallMultipleProtocolInterfaces() to produce potocols and manage other handle devices


---?image=/assets/images/slides/Slide23.JPG
@title[Lab 4: Debugging before Testing the Driver ]
<p align="right"><span class="gold" >Lab 4: Debugging before Testing the Driver</span></p>
<br>
<span style="font-size:0.8em" >UEFI drivers can use the EDK II debug library </span><br>

<div class="left1">
<ul style="list-style-type:none">
  <li>@fa[book gp-bullet-gold]<span style="font-size:0.8em" >&nbsp;&nbsp;`DEBUG( )`	 include - `[DebugLib.h]`</span></li><br>
  <li><span style="font-size:0.8em" >`DEBUG()` Macro statements can show status progress interest points throughout  the driver code</span></li>
</ul>
</div>
<div class="right1">
<span style="font-size:0.8em" >&nbsp;</span>
</div>


---
@title[Lab 4: Add Debug statements supported ]
<p align="right"><span class="gold" >Lab 4: Add Debug Statements `Supported()`</span></p>
<span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > the following  <span style="background-color: #101010">`DEBUG ()` </span> macros for the supported function:</span>
```C
	Status = gBS->OpenProtocol(
		ControllerHandle,
		&gEfiSerialIoProtocolGuid,
		(VOID **)&SerialIo,
		This->DriverBindingHandle,
		ControllerHandle,
		EFI_OPEN_PROTOCOL_BY_DRIVER | EFI_OPEN_PROTOCOL_EXCLUSIVE
		);

	if (EFI_ERROR(Status)) {
	   DEBUG((EFI_D_INFO, "[MyWizardDriver] Not Supported \r\n"));
	   return Status; // Bail out if OpenProtocol returns an error
	}
	
	// We're here because OpenProtocol was a success, so clean up
	gBS->CloseProtocol(
		ControllerHandle,
		&gEfiSerialIoProtocolGuid,
		This->DriverBindingHandle,
		ControllerHandle
		);
	DEBUG((EFI_D_INFO, "[MyWizardDriver] Supported SUCCESS\r\n"));
	return EFI_SUCCESS;
```	
@[11](Copy / Paste DEBUG macro here. The `Status` variable depends on the output of the `OpenProtocol` function.)
@[22](Copy / Paste another DEBUG macro here. It is only display when the Supported function returns EFI_SUCCESS.)



---
@title[Lab 4: Add Debug statements start ]
<p align="right"><span class="gold" >Lab 4: Add Debug Statements `Start()`</span></p>
<br>
<span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > the following <span style="background-color: #101010">`DEBUG`</span> macro for the Start function just before the <span style="background-color: #101010">`return EFI_SUCCESS;` </span>statement</span></span>
```C
  DEBUG ((EFI_D_INFO, "\r\n***\r\n[MyWizardDriver] Buffer 0x%08x\r\n", DummyBufferfromStart));
  return EFI_SUCCESS;
```	
<span style="font-size:0.7em" ><i>Note: </i>This debug macro displays the memory address of the allocated buffer on the debug console</span><br>
<br>

<span style="font-size:0.8em" ><b>Save</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > `C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`</span>



---?image=/assets/images/slides/Slide26.JPG
@title[Lab 4 Build and Test Driver]
<p align="right"><span class="gold" >Lab 4: Build and Test Driver</span></p>
<br>
<p style="line-height:80%"><span style="font-size:0.8em" > Build the MyWizardDriver </span></p>
```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run
```
<p style="line-height:80%"><span style="font-size:0.7em" >Load the UEFI Driver from the shell
<br>&nbsp;&nbsp;&nbsp;<span style="background-color: #101010"><font color="yellow">`Shell> `</font>`fs0:`</span>
<br>&nbsp;&nbsp;&nbsp;<span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`</span></span></p>


Note: 


Same as slide


---?image=/assets/images/slides/Slide27.JPG
@title[Lab 4 Build and Test Driver 02]
<p align="right"><span class="gold" >Lab 4: Build and Test Driver</span></p>
<br>
<div class="left2">
<ul>
  <li><span style="font-size:0.7em" >Check the VS console output.</span></li>
  <li><span style="font-size:0.7em" >Notice Debug messages indicate the driver did not return `EFI_SUCCESS` from the “`Supported()`” function.  </span></li>
  <li><span style="font-size:0.7em" >See that the "`Start()`" function did <b>NOT</b>get called.</span></li>
 
</ul>
<br>
<br>
<span style="font-size:0.7em" >Exit, type <font color="yellow">`FS0:/ >`</font> `Reset`</span><br>
</div>
<div class="right2">
<span style="font-size:0.8em" ></span>
</div>
<br>

Note:
Finished Lab 4

---?image=/assets/images/slides/Slide_LabSec.JPG
@title[Lab 5: Create NV Var Section]
<br>
<br>
<p align="Left"><span class="gold" >Lab 5: Create a NVRAM Variable </span></p>
<br>
<div class="left1">
<ul>
  <li><span style="font-size:0.8em" >In this lab you’ll create a non-volatile UEFI variable (NVRAM), and set and get the variable to return a successful supported function </span></li>
  <li><span style="font-size:0.8em" >Use Runtime services to </span><span style="font-size:0.65em" >"`SetVariable()`" and "`GetVariable()`"</span></li>

</ul>
</div>
<div class="right1">
<span style="font-size:0.8em" >&nbsp;  </span>
</div>
 
Note:

On systems without a serial port, the code from previous lab will not work since the Serial Protocol GUID does not exist. This lab demonstrates another mechanism (also known as “a trick”) to return from the “Supported” function.  

With QEMU there is a serial device so the driver’s start function would then start to manage the serial port by creating child handles. 


---
@title[Lab 5: Create NV Var steps]
<br>
<p align="center"><span class="gold" >Lab 5: Adding a NVRAM Variable Steps </span></p>
<br>
<ol style="line-height:0.9;">
  <li><span style="font-size:0.8em" >Create .h file with new <font color="#87b7e4">`typedef`</font> definition and its own <font color="#87b7e4">`GUID`</font> </span></li>
  <li><span style="font-size:0.8em" >Include the new .h file in the driver's top .h file </span></li>
  <li><span style="font-size:0.8em" >`EntryPoint()` Init new buffer for NVRam Variable   </span></li>
  <li><span style="font-size:0.8em" >`Supported()` make a call to a new function to set/get the new NVRam Variable  </span></li>
  <li><span style="font-size:0.8em" >Before `EntryPoint()` add the new function `CreateNVVariable()` to the driver.c file.</span></li>

</ol>



---
@title[Lab 5: Create a new .h file ]
<p align="right"><span class="gold" >Lab 5: Create a new .h file</span></p>
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Create</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > a new file in your editor called: "`MyWizardDriverNVDataStruc.h`"</span><br>
<span style="font-size:0.8em" ><b>Copy, Paste</b> and then <b>Save</b> this file</b>&nbsp;&nbsp;</span></p>
```C++
#ifndef _MYWIZARDDRIVERNVDATASTRUC_H_
#define _MYWIZARDDRIVERNVDATASTRUC_H_
#include <Guid/HiiPlatformSetupFormset.h>
#include <Guid/HiiFormMapMethodGuid.h>

#define MYWIZARDDRIVER_VAR_GUID \
  { \
	0x363729f9, 0x35fc, 0x40a6, 0xaf, 0xc8, 0xe8, 0xf5, 0x49, 0x11, 0xf1, 0xd6 \
  }

#pragma pack(1)
typedef struct {

    UINT16  MyWizardDriverStringData[20];
    UINT8   MyWizardDriverHexData;
    UINT8   MyWizardDriverBaseAddress;
    UINT8   MyWizardDriverChooseToEnable;
 
} MYWIZARDDRIVER_CONFIGURATION;

#pragma pack()

#endif

```

Note:

- In order to set, retrieve, and use the UEFI variable, it requires the GUID reference that you just added.

- another Note:  For this lab, you were provided a GUID file.  You can also generate a GUID through the UEFI Driver Wizard or Guidgenerator.com.  But for the purposes of the lab, use the one above.



---
@title[Lab 5: Add New Vars to .c ]
<p align="right"><span class="gold" >Lab 5: Update MyWizardDriver.c</span></p>
<br>
<span style="font-size:0.8em" ><b>Open</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`"</span><br>
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the following  4 lines after the `#include "MyWizardDriver.h"` statement: </span></p>
```C
#include "MyWizardDriver.h"

EFI_GUID   mMyWizardDriverVarGuid = MYWIZARDDRIVER_VAR_GUID;

CHAR16     mVariableName[] = L"MWD_NVData";  // Use Shell "Dmpstore" to see 
MYWIZARDDRIVER_CONFIGURATION   mMyWizDrv_Conf_buffer;
MYWIZARDDRIVER_CONFIGURATION   *mMyWizDrv_Conf = &mMyWizDrv_Conf_buffer;  //use the pointer 
```

Note:
Same as slide

---
@title[Lab 5: Update Suppport for new function ]
<p align="right"><span class="gold" >Lab 5: Update MyWizardDriver.c</span></p>
<br>
<span style="font-size:0.8em" ><b>Locate</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > "`MyWizardDriverDriverBindingSupported ()`" function</span><br>
<span style="font-size:0.8em" ><b>Comment out</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the `DEBUG` macro statement and return statement as below: </span><br>
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the 7 lines: 1) new call to "`CreateNVVariable();`" 2-6) `if` statement with DEBUG and 7) "`return`"  as below: </span></p>

```C
	if (EFI_ERROR(Status)) {
		//DEBUG((EFI_D_INFO, "[MyWizardDriver] Not Supported \r\n"));
		//return Status; // Bail out if OpenProtocol returns an error
		Status = CreateNVVariable();
		if (EFI_ERROR(Status)) {
           DEBUG((EFI_D_ERROR, "[MyWizardDriver] Not Supported \r\n"));
        }else{
           DEBUG((EFI_D_ERROR, "[MyWizardDriver] Supported \r\n"));
        }
        return Status; // Status now depends on CreateNVVariable Function
```

Note:

copy paste


---
@title[Lab 5: Add new function ]
<p align="right"><span class="gold" >Lab 5: Update MyWizardDriver.c</span></p>
<span style="font-size:0.7em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.5em" > the new function before the call to 
      "`MyWizardDriverDriverEntryPoint()`" </span>
```c
EFI_STATUS
EFIAPI
CreateNVVariable()
{
	EFI_STATUS            	Status;
	UINTN                  BufferSize;

	BufferSize = sizeof (MYWIZARDDRIVER_CONFIGURATION);
	Status = gRT->GetVariable(
		mVariableName,
		&mMyWizardDriverVarGuid,
		NULL,
		&BufferSize,
		mMyWizDrv_Conf
		);
	if (EFI_ERROR(Status)) {  // Not definded yet so add it to the NV Variables.
		if (Status == EFI_NOT_FOUND) {
			Status = gRT->SetVariable(
				mVariableName,
				&mMyWizardDriverVarGuid,
				EFI_VARIABLE_NON_VOLATILE | EFI_VARIABLE_BOOTSERVICE_ACCESS,
				sizeof (MYWIZARDDRIVER_CONFIGURATION),
				mMyWizDrv_Conf   //  buffer is 000000  now for first time set
				);
			DEBUG((EFI_D_INFO, "[MyWizardDriver] Variable %s created in NVRam Var\r\n", mVariableName));
			return EFI_SUCCESS;
		}
	}
	// already defined once 
	return EFI_UNSUPPORTED;
}
```	  


---
@title[Lab 5: Update .h]
<p align="right"><span class="gold" >Lab 5: Update MyWizardDriver.h</span></p>
<span style="font-size:0.8em" ><b>Open</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.h`"</span><br>
<p style="line-height:70%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the following "#include" after the list of library include statements: </span></p>
```C++
// Libraries
// . . .
#include <Library/UefiRuntimeServicesTableLib.h>
```
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the following  "#include" after the list of protocol include statements: </span></p>
```C++
// Produced Protocols
// . . .
#include "MyWizardDriverNVDataStruc.h"	
```
<span style="font-size:0.8em" ><b>Save</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.h`"</span><br>
<span style="font-size:0.8em" ><b>Save</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`"</span>	  

Note:

---?image=/assets/images/slides/Slide35.JPG
@title[Lab 5 Build and Test Driver]
<p align="right"><span class="gold" >Lab 5: Build and Test Driver</span></p>

<p style="line-height:80%"><span style="font-size:0.8em" > Build the MyWizardDriver </span></p>
<div class="left">
<pre>
```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run

```
</pre>
<span style="font-size:0.8em" ><b>Load</b> the UEFI Driver </span><br>
<span style="font-size:0.5em" >&nbsp;&nbsp;&nbsp;<span style="background-color: #101010"><font color="yellow">`Shell> `</font>`fs0:`</span></span><br>
<span style="font-size:0.5em" >&nbsp;&nbsp;&nbsp;<span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`</span></span><br>
<span style="font-size:0.7em" >Observe the Buffer address returned by the debug statement in the VS Command window</span></span><br>
<span style="font-size:0.7em" ></span><br>

</div>
<div class="right">
<span style="font-size:0.8em" ></span>
</div>

Note:



---?image=/assets/images/slides/Slide36.JPG
@title[Lab 5 Verify Driver]
<p align="right"><span class="gold" >Lab 5: Verify Driver</span></p>
<br>
<span style="font-size:0.75em" >At the Shell prompt, type&nbsp;&nbsp; <span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`mem 0x0587f010`</span></span><br>
<span style="font-size:0.75em" >Observe the Buffer is filled with the letter "B" or 0x0042 </span></span><br>
<br>
<br>
<br>
<br>



Note:

Same as slide



---?image=/assets/images/slides/Slide42.JPG
@title[Lab 5 Verify NVRAM Driver]
<p align="right"><span class="gold" >Lab 5: Verify NVRAM Created by Driver</span></p>
<br>
<span style="font-size:0.7em" >At the Shell prompt, type &nbsp;&nbsp;<span style="background-color: #101010"><font color="yellow">`FS0:\> `</font>`dmpstore -all -b`</span></span><br>
<div class="left1">
<span style="font-size:0.65em" >Observe new the NVRAM variable "`MWD_NVData`" was created and filled with 0x00s</span></span><br>
<br>
<br>
<br>
<br>
<br>
<br>
<span style="font-size:0.7em" >Exit, type <font color="yellow">`FS0:/ >`</font> `Reset`</span><br>
</div>
<div class="right1">
<span style="font-size:0.8em" ></span>
</div>
Note:

End of Lab 5



---?image=/assets/images/slides/Slide_LabSec.JPG
@title[Lab 6: Port Stop and Unload]
<br>
<br>
<p align="Left"><span class="gold" >Lab 6: Port Stop and Unload </span></p>
<br>
<div class="left1">
<span style="font-size:0.8em" >In this lab, you’ll port the driver’s “Unload” and “Stop” functions to free any resources the driver allocated when it was loaded and started.</span>
</div>
<div class="right1">
<span style="font-size:0.8em" >&nbsp;  </span>
</div>
 
Note:


---
@title[Lab 6: Port the Unload]
<p align="right"><span class="gold" >Lab 6: Port the Unload function</span></p>
<br>
<span style="font-size:0.8em" ><b>Open</b>&nbsp;&nbsp;</span><span style="font-size:0.7em" > "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`"</span><br>
<span style="font-size:0.8em" ><b>Locate</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > "`MyWizardDriverUnload ()`" function</span><br>
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the following "`if`"  and "`DEBUG`" statements before the "`return EFI_SUCCESS;`" statement.</span></p>
```C++
  // Do any additional cleanup that is required for this driver
  //
  if (DummyBufferfromStart != NULL) {
	  FreePool(DummyBufferfromStart);
	  DEBUG((EFI_D_INFO, "[MyWizardDriver] Unload, clear buffer\r\n"));
  }
  DEBUG((EFI_D_INFO, "[MyWizardDriver] Unload success\r\n"));

  return EFI_SUCCESS;
```

Note:

- The code will deallocate the buffer using the FreePool library function.
- Notice that the FreePool is called since there was an allocat call to get memory in the start function
- for the Unload similar "unwind" calls such as
  - free memory
  - Uninstall Protocol Interfaces
  - Disconnect Controller calls are made
  

---
@title[Lab 6: Port the Stop]
<p align="right"><span class="gold" >Lab 6: Port the Stop function</span></p>
<span style="font-size:0.8em" ><b>Locate</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > "`MyWizardDriverDriverBindingStop()`" function</span><br>
<span style="font-size:0.8em" ><b>Comment out</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > with "`//`" before the "`return EFI_UNSUPPORTED;`" statement.</span><br>
<p style="line-height:80%"><span style="font-size:0.8em" ><b>Copy & Paste</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" > the following "`if`"  and "`DEBUG`" statements in place of the "`return EFI_UNSUPPORTED;`" statement.</span></p>
```C++
	if (DummyBufferfromStart != NULL) {
		FreePool(DummyBufferfromStart);
		DEBUG((EFI_D_INFO, "[MyWizardDriver] Stop, clear buffer\r\n"));
	}

	DEBUG((EFI_D_INFO, "[MyWizardDriver] Stop, EFI_SUCCESS\r\n"));
	return EFI_SUCCESS;
  //  return EFI_UNSUPPORTED;
}
```
<span style="font-size:0.8em" ><b>Save & Close</b>&nbsp;&nbsp;</span><span style="font-size:0.65em" >"`MyWizardDriverDriver.c`"</span>

Note:

- The code will deallocate the buffer using the FreePool library function.
- This a duplicate of the check performed in the unload function, in case the stop function was executed prior to unload.
- Notice that the FreePool is called since there was an allocat call to get memory in the start function
- for the stop similar "unwind" calls to mimic same functions in the start
  - free memory for Alocate memory
  - Uninstall Protocol Interfaces  for Install interfaces
  
    

---?image=/assets/images/slides/Slide41.JPG
@title[Lab 6 Build and Test Driver]
<p align="right"><span class="gold" >Lab 6: Build and Test Driver</span></p>
<div class="left1">
<p style="line-height:80%"><span style="font-size:0.8em" > Build the MyWizardDriver </span></p>
<pre>
```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run
```
</pre>
<span style="font-size:0.8em" ><b>Load</b> the UEFI Driver </span><br>
<span style="font-size:0.5em" >&nbsp;&nbsp;&nbsp;<span style="background-color: #101010"><font color="yellow">`Shell> `</font>`fs0:`</span></span><br>
<span style="font-size:0.5em" >&nbsp;&nbsp;&nbsp;<span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`</span></span><br>
<span style="font-size:0.7em" >Observe the Buffer address is at `0x0587f010` as this slide example</span><br>

</div>
<div class="right1">
<span style="font-size:0.8em" ></span>
</div>

Note:

Same as slide




---?image=/assets/images/slides/Slide42.JPG
@title[Lab 6 Verify Driver]
<p align="right"><span class="gold" >Lab 6: Verify Driver</span></p>
<br>
<span style="font-size:0.7em" >At the Shell prompt, type &nbsp;<span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`drivers`</span></span><br>
<br>
<div class="left1">
<span style="font-size:0.7em" >Observe the handle is "`A9`" as this slide example </span><br>
<span style="font-size:0.7em" >Type: &nbsp;<span style="background-color: #101010">` mem  0x0587f010`</span></span><br>
<span style="font-size:0.7em" >Observe the buffer was filled with the "0x0042" </span><br>
</div>
<div class="right1">
<span style="font-size:0.8em" ></span>
</div>

Note:

Same as slide




---?image=/assets/images/slides/Slide43.JPG
@title[Lab 6 Verify Unload]
<p align="right"><span class="gold" >Lab 6: Verify Unload</span></p>
<br>
<span style="font-size:0.7em" >At the Shell prompt, type &nbsp;<span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`unload a9`</span></span><br>
<br>
<div class="left1">
<span style="font-size:0.7em" >Observe the DEBUG messages from the Unload</span><br><br>
<span style="font-size:0.7em" >Type `Drivers` again to verify</span><br>
</div>
<div class="right1">
<span style="font-size:0.8em" ></span>
</div>

Note:

Same as slide
        



---?image=/assets/images/slides/Slide44.JPG
@title[Lab 6 Verify Unload]
<p align="right"><span class="gold" >Lab 6: Verify Unload</span></p>
<br>
<span style="font-size:0.7em" > At the Shell prompt, type &nbsp;<span style="background-color: #101010"><font color="yellow">`FS0:\> `&nbsp;</font>`mem 0x0587f010  -b`</span></span><br>
<br>
<div class="left1">
<span style="font-size:0.7em" >Observe the buffer is now NOT filled </span><br>
<br>
<br>
<br>
<br>
<br>
<span style="font-size:0.7em" >Exit, type <font color="yellow">`FS0:/ >`</font> `Reset`</span><br>
</div>
<div class="right1">
<span style="font-size:0.8em" ></span>
</div>

Note:

Same as slide
     
  


---  
@title[Summary]
<BR>
### <p align="center"><span class="gold"   >Summary </span></p><br>
<ul style="list-style-type:none">
 <li>@fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Compile a UEFI driver template created from<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; UEFI Driver Wizard</span> </li><br>
 <li>@fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Test driver w/ Nt32 emulation using UEFI Shell 2.0</span></li><br>
 <li>@fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Port code into the template driver</span> </li>
</ul>

---?image=assets/images/gitpitch-audience.jpg
@title[Questions]
<br>
![Questions](/assets/images/questions.JPG) 


---?image=assets/images/gitpitch-audience.jpg
@title[Logo Slide]
<br><br><br>
![Logo Slide](/assets/images/TianocoreLogo.png =10x)


---
@title[Acknowledgements]
#### <p align="center"><span class="gold"   >Acknowledgements</span></p>

```c++
/**
Redistribution and use in source (original document form) and 'compiled' forms (converted
to PDF, epub, HTML and other formats) with or without modification, are permitted provided
that the following conditions are met:

Redistributions of source code (original document form) must retain the above copyright 
notice, this list of conditions and the following disclaimer as the first lines of this 
file unmodified.

Redistributions in compiled form (transformed to other DTDs, converted to PDF, epub, HTML
and other formats) must reproduce the above copyright notice, this list of conditions and 
the following disclaimer in the documentation and/or other materials provided with the 
distribution.

THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR IMPLIED 
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND 
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL TIANOCORE PROJECT BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES 
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, 
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF ADVISED OF THE POSSIBILITY 
OF SUCH DAMAGE.

Copyright (c) 2018, Intel Corporation. All rights reserved.
**/

```
