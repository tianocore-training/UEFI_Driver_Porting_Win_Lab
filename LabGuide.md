
## Slide 1
# UEFI & EDK II Training

## How to Write a UEFI Driver Lab - Windows


---  
## Slide 2 @title[Lesson Objective]
<p align="center">Lesson Objective </p><br>
<ul>
 <li>Compile a UEFI driver template created fromUEFI Driver Wizard </li>
 <li>Test driver w/ Nt32 emulation using UEFI Shell 2.0</li>
 <li>Port code into the template driver </li>
</ul>

---?image=assets/images/binary-strings-black2.jpg
## Slide 3 @title[UEFI Driver Lab]


---?image=/assets/images/slides/Slide_LabSec.JPG
## Slide 4 @title[Lab 2: Building a UEFI Driver]
<br>
<br>
<p align="Left">Lab 2: Building a UEFI Driver</p>
<br>

In this lab, you’ll build a UEFI Driver created by the UEFI Driver Wizard.<br>
You will include the driver in the Nt32 project. <br>Build the UEFI Driver from the Driver Wizard 


---?image=/assets/images/slides/Slide5.JPG
## Slide 5 @title[Compile a UEFI Driver?]
<p align="right">Compile a UEFI Driver</p>



---
## Slide 6 @title[Lab2: Build the UEFI Driver?]
<p align="right"><span class="gold" >Lab 2: Build the UEFI Driver</span></p>
<br>
<ul>
   <li>Perform <a href="https://gitpitch.com/tianocore-training/Platform_Build_Win_Lab/master#/9">Lab Setup</a> from previous Nt32Pkg Labs </li>
   <li>Open `C:/FW/edk2/Nt32Pkg/Nt32Pkg.dsc`</li>
   <li>Add the following to the `[Components]` section: </span><br><span style="font-size:0.9em" >*Hint:*add to the last module in the `[Components]` section  </li>

```
    # Add new modules here
     MyWizardDriver/MyWizardDriver.inf
```

   <li>Save and close the file `C:/FW/edk2/Nt32Pkg/Nt32Pkg.dsc`  </li>
</ul>



---
## Slide 7 @title[Lab 2 Build and Test Driver]
<p align="right">Lab 2: Build and Test Driver</p>
Open a VS  Command Prompt and type: `cd C:/FW/edk2` then </span>

```
  C:/FW/edk2> edksetup
```

Build `MyWizardDriver` </p>

```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run
```

Load the UEFI Driver from the shell
<br>&nbsp;&nbsp;&nbsp; At the Shell prompt, type &nbsp;<font color="gray">`Shell> `</font>`fs0:`
<br>&nbsp;&nbsp;&nbsp; Type:&nbsp;<font color="gray">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`<br>
<b>Build ERRORS:</b> Copy the solution files from `~/FW/LabSampleCode/LabSolutions/LessonC.1` to `C:/FW/edk2/MyWizardDriver`	




---?image=/assets/images/slides/Slide8.JPG
## Slide 8 @title[Lab 2 Test Driver Drivers]
<p align="right">Lab 2: Test Driver</p>
<br>
At the shell prompt Type: `drivers`<br>
Verify the UEFI Shell loaded the new driver. 
The `drivers` command will display the driver information and a driver handle number ("a9" in the example screenshot )</span>






---?image=/assets/images/slides/Slide9.JPG
## Slide 9 @title[Lab 2 Test Driver -Dh]
<p align="right"><span class="gold" >Lab 2: Test Driver</span></p>
<br>
At the shell prompt using the handle from the `drivers` command, Type:&nbsp; `dh -d a9`


<i>Note:</i>  The value `a9` is the driver handle for MyWizardDriver.  The handle value may change based on your system configuration.(see example screenshot - right)



Note:

Same as slide




---?image=/assets/images/slides/Slide10.JPG
## Slide 10 @title[Lab 2 Test Driver -unload]
<p align="right">Lab 2: Test Driver</p>
<br>
At the shell prompt using the handle from the `drivers` command, Type:&nbsp; `unload a9`


See example screenshot - right<br>
Type:&nbsp; `drivers` again<br><br>
Notice results of `unload` command<br><br>
Exit, type <font color="gray">`FS0:/ >`</font> `Reset`<br>

Note:


END of Lab 2


---?image=/assets/images/slides/Slide_LabSec.JPG
## Slide 11 @title[Lab 3: Component Name Section]
<br>
<br>
<p align="Left">Lab 3: Component Name</p>

In this lab, you’ll change the information reported to the drivers command using the ComponentName and ComponentName2 protocols.


---
## Slide 12 @title[Lab 3: Component Name ]
<p align="right">Lab 3: Component Name</p>
<br>

- <b>Open</b>&nbsp;&nbsp;`C:/FW/edk2/MyWizardDriver/ComponentName.c`
- <b>Change</b>&nbsp;&nbsp; the string returned by the driver from `MyWizardDriver` to: &nbsp;&nbsp;&nbsp; <font color="black">`UEFI Sample Driver`</font>

   
```
  /// Table of driver names
  ///
 GLOBAL_REMOVE_IF_UNREFERENCED 
 EFI_UNICODE_STRING_TABLE mMyWizardDriverDriverNameTable[] = {
   { "eng;en", (CHAR16 *)L"UEFI Sample Driver" },
   { NULL, NULL }
 };
```

- <b>Save</b> and close the file: `C:/FW/edk2/MyWizardDriver/ComponentName.c`  



---?image=/assets/images/slides/Slide13.JPG
## Slide 13 @title[Lab 3 Build and Test Driver]
<p align="right">Lab 3: Build and Test Driver</p>
<br>
Build the MyWizardDriver 

```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run
```

- Load the UEFI Driver from the shell<br>
- &nbsp;&nbsp;&nbsp; At the Shell prompt, type &nbsp;<font color="gray">`Shell> `</font>`fs0:`<br>
- &nbsp;&nbsp;&nbsp; Type:&nbsp; <font color="gray">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`</span></p>

Type:&nbsp; `drivers`<br>
Observe the change in the string that the driver returned <br>
<br>
Exit, type <font color="gray">`FS0:/ >`</font> `Reset`


Note: 
Lab 3 finished


---?image=/assets/images/slides/Slide_LabSec.JPG
## Slide 14 @title[Lab 4: Port Supported Section]
<br>
<br>
<p align="Left">Lab 4: Porting the Supported & Start Functions</p>
<br>
The UEFI Driver Wizard produced a starting point for driver porting … so now what?<br><br>
In this lab, you’ll port the “Supported” and “Start” functions for the UEFI driver



---?image=/assets/images/slides/Slide15.JPG
## Slide 15 @title[Lab 4: Port Supported-Start]
<p align="center">Lab 4: Porting Supported and Start</p>
<span style="font-size:01.1em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>Review the Driver Binding Protocol</b></span>

Note:

- Port Supported() to check for a specific protocol before returning ‘Success’
- Port Start() to allocate a memory buffer and fill it with a specific value

---
## Slide 16 @title[Lab 4: Supported Port]
<p align="right">Lab 4: The `Supported()` Port</p>
The UEFI Driver Wizard produced a `Supported()` function but it only returns `EFI_UNSUPPORTED` </span></p>

<Font color="red"><b>Supported Goals: </b></font> 

- Checks if the driver supports the device for the specified controller handle 
- Associates the driver with the Serial I/O protocol 
- Helps locate a protocol’s specific GUID through  UEFI Boot Services’ function 


Note: 

Same as slide


---?image=/assets/images/slides/Slide17.JPG
## Slide 17 @title[Lab 4: Help from Robust Libraries]
<p align="right">Lab 4: Help from Robust Libraries</p>
EDK II has libraries to help with porting UEFI Drivers <br>

- `AllocateZeroPool()` include - `[MemoryAllocationLib.h]`  
- `SetMem16()`   include - `[BaseMemoryLib.h]`  
</ul>
<br>
<br>
<br>
Check the MdePkg with libraries help file (.chm format) 


Note: 

---
## Slide 18 @title[Lab 4: Update Supported ]
<p align="right">Lab 4: Update Supported</p>


<b>Open</b>&nbsp;&nbsp;`C:/FW/edk2/MyWizardDriver/MyWizardDriver.c` <br>
<b>Locate</b>&nbsp;&nbsp; ` MyWizardDriverDriverBindingSupported()`, 
       the supported function for this driver and comment out the "`//`" in the line: "`return EFI_UNSUPPORTED;` " 

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

<b>copy</b> and past (next slide)

Note: 

This code checks for a specific protocol before returning a status for the supported function (EFI_SUCCESS if the protocol GUID exists).


---
## Slide 19 @title[Lab 4: Update Supported 02 ]
<p align="right">Lab 4: Update Supported Add Code </p>
<b>Copy & Paste</b>&nbsp;&nbsp; the following code for the supported function `MyWizardDriverDriverBindingSupported()`:

<hr>

```
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

Note:
  end of copy & paste

---
## Slide 20 @title[Lab 4: Notice UEFI Driver Wizard Includes  ]
<p align="right">Lab 4: Notice UEFI Driver Wizard Includes</p>

- <b>Open</b>&nbsp;&nbsp;`C:/FW/edk2/MyWizardDriver/MyWizardDriver.h`
- <b>Notice</b>&nbsp;&nbsp; the following include statement is already added by the driver wizard: 

```
// Produced Protocols
//
#include <Protocol/SerialIo.h>

```

- <b>Review</b>&nbsp;&nbsp; the Libraries section and see that UEFI Driver Wizard automatically includes library headers based on the form information. Also other common libary headers were included 

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



Note: 


---
## Slide 21 @title[Lab 4: Update the Start  ]
<p align="right">Lab 4: Update the `Start()` </p>

<b>Copy & Paste</b>&nbsp;&nbsp; the following in  `MyWizardDriver.c` after the <br>`#include “MyWizardDriver.h”` line

```
#define  DUMMY_SIZE 100*16		// Dummy buffer
CHAR16	*DummyBufferfromStart = NULL;

```

<b>Locate</b>&nbsp;&nbsp;` MyWizardDriverDriverBindingStart()`,  the start function for this driver and comment out the "`//`" in the line "`return EFI_UNSUPPORTED;` "</span></li>

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



Note: 


---
## Slide 22 @title[Lab 4: Update Start 02 ]
<p align="right">Lab 4: Update Start Add Code </p>
<b>Copy & Paste</b>&nbsp;&nbsp; the following code for the start function ` MyWizardDriverDriverBindingStart()`:

```
	if (DummyBufferfromStart == NULL) {     // was buffer already allocated?
		DummyBufferfromStart = (CHAR16*)AllocateZeroPool (DUMMY_SIZE * sizeof(CHAR16));
	}

	if (DummyBufferfromStart == NULL) {
		return EFI_OUT_OF_RESOURCES;    // Exit if the buffer isn’t there
	}

	SetMem16 (DummyBufferfromStart, (DUMMY_SIZE * sizeof(CHAR16)), 0x0042);  // Fill buffer

	return EFI_SUCCESS;
```
- Notice the Library calls to `AllocateZeroPool()` and `SetMem16()`
- The `Start()` function is where there would be calls to "`gBS->InstallMultipleProtocolInterfaces()`"


Note:

- This code checks for an allocated memory buffer. If the buffer doesn’t exist, memory will be allocated and filled with an initial value (0x0042). 
- this lab's start does **not** do anything useful but if it did it would make calls to gBS->InstallMultipleProtocolInterfaces() to produce potocols and manage other handle devices


---?image=/assets/images/slides/Slide23.JPG
## Slide 23 @title[Lab 4: Debugging before Testing the Driver ]
<p align="right">Lab 4: Debugging before Testing the Driver</p>
<br>
UEFI drivers can use the EDK II debug library 

- `DEBUG( )`	 include - `[DebugLib.h]`<br>
- `DEBUG()` Macro statements can show status progress interest points throughout  the driver code

---
## Slide 24 @title[Lab 4: Add Debug statements supported ]
<p align="right">Lab 4: Add Debug Statements `Supported()`</p>
<b>Copy & Paste</b>&nbsp;&nbsp; the following  `DEBUG ()`  macros for the supported function:

```
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
## Slide 25 @title[Lab 4: Add Debug statements start ]
<p align="right">Lab 4: Add Debug Statements `Start()`</p>
<br>
<b>Copy & Paste</b>&nbsp;&nbsp; the following `DEBUG` macro for the Start function just before the `return EFI_SUCCESS;` statement

```
  DEBUG ((EFI_D_INFO, "\r\n***\r\n[MyWizardDriver] Buffer 0x%08x\r\n", DummyBufferfromStart));
  return EFI_SUCCESS;
```	

<i>Note: </i>This debug macro displays the memory address of the allocated buffer on the debug console<br>
<br>

<b>Save</b>&nbsp;&nbsp; `C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`



---?image=/assets/images/slides/Slide26.JPG
## Slide 26 @title[Lab 4 Build and Test Driver]
<p align="right">Lab 4: Build and Test Driver</p>
<br>
Build the MyWizardDriver 

```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run

```
Load the UEFI Driver from the shell<br>
&nbsp;&nbsp;&nbsp;<font color="gray">`Shell> `</font>`fs0:`<br>
&nbsp;&nbsp;&nbsp;<font color="gray">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`


Note: 


Same as slide


---?image=/assets/images/slides/Slide27.JPG
## Slide 27 @title[Lab 4 Build and Test Driver 02]
<p align="right">Lab 4: Build and Test Driver</p>

- Check the VS console output.
- Notice Debug messages indicate the driver did not return `EFI_SUCCESS` from the “`Supported()`” function. 
- See that the "`Start()`" function did <b>NOT</b>get called.
<br>
<br>
Exit, type <font color="gray">`FS0:/ >`</font> `Reset`</span><br>
<br>

Note:
Finished Lab 4

---?image=/assets/images/slides/Slide_LabSec.JPG
## Slide 28 @title[Lab 5: Create NV Var Section]
<br>
<br>
<p align="Left">Lab 5: Create a NVRAM Variable </p>
<br>


- In this lab you’ll create a non-volatile UEFI variable (NVRAM), and set and get the variable to return a successful supported function 
- Use Runtime services to "`SetVariable()`" and "`GetVariable()`"


 
Note:

On systems without a serial port, the code from previous lab will not work since the Serial Protocol GUID does not exist. This lab demonstrates another mechanism (also known as “a trick”) to return from the “Supported” function.  

With QEMU there is a serial device so the driver’s start function would then start to manage the serial port by creating child handles. 


---
## Slide 29 @title[Lab 5: Create NV Var steps]
<br>
<p align="center">Lab 5: Adding a NVRAM Variable Steps </p>
<br>
<ol>
  <li>Create .h file with new <font color="#87b7e4">`typedef`</font> definition and its own <font color="#87b7e4">`GUID`</font> </li>
  <li>Include the new .h file in the driver's top .h file </li>
  <li>`EntryPoint()` Init new buffer for NVRam Variable   </li>
  <li>`Supported()` make a call to a new function to set/get the new NVRam Variable  </li>
  <li>Before `EntryPoint()` add the new function `CreateNVVariable()` to the driver.c file.</li>

</ol>



---
## Slide 30 @title[Lab 5: Create a new .h file ]
<p align="right">Lab 5: Create a new .h file</p>
<b>Create</b>&nbsp;&nbsp;</span><span style="font-size:0.9em" > a new file in your editor called: "`MyWizardDriverNVDataStruc.h`"</span><br>
<b>Copy, Paste</b> and then <b>Save</b> this file</b>&nbsp;&nbsp;</span></p>

<hr>

```
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

<hr>
Note:

- In order to set, retrieve, and use the UEFI variable, it requires the GUID reference that you just added.

- another Note:  For this lab, you were provided a GUID file.  You can also generate a GUID through the UEFI Driver Wizard or Guidgenerator.com.  But for the purposes of the lab, use the one above.



---
## Slide 31 @title[Lab 5: Add New Vars to .c ]
<p align="right">Lab 5: Update MyWizardDriver.c</span></p>
<br>
<b>Open</b>&nbsp;&nbsp;</span><span style="font-size:0.9em" > "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`"<br>
<b>Copy & Paste</b>&nbsp;&nbsp; the following  4 lines after the `#include "MyWizardDriver.h"` statement: 

```
#include "MyWizardDriver.h"

EFI_GUID   mMyWizardDriverVarGuid = MYWIZARDDRIVER_VAR_GUID;

CHAR16     mVariableName[] = L"MWD_NVData";  // Use Shell "Dmpstore" to see 
MYWIZARDDRIVER_CONFIGURATION   mMyWizDrv_Conf_buffer;
MYWIZARDDRIVER_CONFIGURATION   *mMyWizDrv_Conf = &mMyWizDrv_Conf_buffer;  //use the pointer 

```

Note:
Same as slide

---
## Slide 32 @title[Lab 5: Update Suppport for new function ]
<p align="right">Lab 5: Update MyWizardDriver.c</p>
<br>
<b>Locate</b>&nbsp;&nbsp;</span><span style="font-size:0.9em" > "`MyWizardDriverDriverBindingSupported ()`" function<br>
<b>Comment out</b>&nbsp;&nbsp; the `DEBUG` macro statement and return statement as below:<br>
<b>Copy & Paste</b>&nbsp;&nbsp; the 7 lines: 1) new call to "`CreateNVVariable();`" 2-6) `if` statement with DEBUG and 7) "`return`"  as below: 

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
## Slide 33 @title[Lab 5: Add new function ]
<p align="right">Lab 5: Update MyWizardDriver.c</p>
<b>Copy & Paste</b>&nbsp;&nbsp; the new function before the call to `MyWizardDriverDriverEntryPoint()`
<br>
<hr>

```

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
## Slide 34 @title[Lab 5: Update .h]
<p align="right">Lab 5: Update MyWizardDriver.h</p>
<b>Open</b>&nbsp;&nbsp; "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.h`"<br>
<b>Copy & Paste</b>&nbsp;&nbsp; the following "#include" after the list of library include statements:

```C++

 // Libraries
 // . . .
 #include <Library/UefiRuntimeServicesTableLib.h>
```
<br>
<b>Copy & Paste</b>&nbsp;&nbsp; the following  "#include" after the list of protocol include statements: 

```C++
 // Produced Protocols
 // . . .
 #include "MyWizardDriverNVDataStruc.h"	

 ```
<b>Save</b>&nbsp;&nbsp; "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.h`"<br>
<b>Save</b>&nbsp;&nbsp; "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`"	  

Note:

---?image=/assets/images/slides/Slide35.JPG
## Slide 35 @title[Lab 5 Build and Test Driver]
<p align="right">Lab 5: Build and Test Driver</p>

Build the MyWizardDriver 


```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run

```

<b>Load</b> the UEFI Driver </span><br>
&nbsp;&nbsp;&nbsp;<font color="gray">`Shell> `</font>`fs0:`</span><br>
&nbsp;&nbsp;&nbsp;<font color="gray">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`</span><br>
Observe the Buffer address returned by the debug statement in the VS Command window</span></span><br>




Note:



---?image=/assets/images/slides/Slide36.JPG
## Slide 36 @title[Lab 5 Verify Driver]
<p align="right">Lab 5: Verify Driver</p>
<br>
At the Shell prompt, type&nbsp;&nbsp; <font color="gray">`FS0:\> `&nbsp;</font>`mem 0x0587f010`<br>
Observe the Buffer is filled with the letter "B" or 0x0042 <br>
<br>
<br>
<br>
<br>



Note:

Same as slide



---?image=/assets/images/slides/Slide42.JPG
## Slide 37 @title[Lab 5 Verify NVRAM Driver]
<p align="right">Lab 5: Verify NVRAM Created by Driver</p>
<br>
At the Shell prompt, type &nbsp;&nbsp;<font color="gray">`FS0:\> `</font>`dmpstore -all -b`<br>

Observe new the NVRAM variable "`MWD_NVData`" was created and filled with 0x00s<br>
<br>
<br>
<br>
<br>
<br>
<br>
Exit, type <font color="gray">`FS0:/ >`</font> `Reset`

Note:

End of Lab 5



---?image=/assets/images/slides/Slide_LabSec.JPG
## Slide 38 @title[Lab 6: Port Stop and Unload]
<br>
<br>
<p align="Left">Lab 6: Port Stop and Unload </p>
<br>
<div class="left1">
In this lab, you’ll port the driver’s “Unload” and “Stop” functions to free any resources the driver allocated when it was loaded and started.

 
Note:


---
## Slide 39 @title[Lab 6: Port the Unload]
<p align="right">Lab 6: Port the Unload function</p>
<br>
<b>Open</b>&nbsp;&nbsp; "`C:/FW/edk2/MyWizardDriver/MyWizardDriver.c`"<br>
<b>Locate</b>&nbsp;&nbsp;"`MyWizardDriverUnload ()`" function<br>
<b>Copy & Paste</b>&nbsp;&nbsp;the following "`if`"  and "`DEBUG`" statements before the "`return EFI_SUCCESS;`" statement.

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
## Slide 40 @title[Lab 6: Port the Stop]
<p align="right">Lab 6: Port the Stop function</p>
<b>Locate</b>&nbsp;&nbsp;"`MyWizardDriverDriverBindingStop()`" function<br>
<b>Comment out</b>&nbsp;&nbsp; with "`//`" before the "`return EFI_UNSUPPORTED;`" statement.<br>
<b>Copy & Paste</b>&nbsp;&nbsp; the following "`if`"  and "`DEBUG`" statements in place of the "`return EFI_UNSUPPORTED;`" statement.</p>

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

<b>Save & Close</b>&nbsp;&nbsp;"`MyWizardDriverDriver.c`"

Note:

- The code will deallocate the buffer using the FreePool library function.
- This a duplicate of the check performed in the unload function, in case the stop function was executed prior to unload.
- Notice that the FreePool is called since there was an allocat call to get memory in the start function
- for the stop similar "unwind" calls to mimic same functions in the start
  - free memory for Alocate memory
  - Uninstall Protocol Interfaces  for Install interfaces
  
    

---?image=/assets/images/slides/Slide41.JPG
## Slide 41 @title[Lab 6 Build and Test Driver]
<p align="right">Lab 6: Build and Test Driver</span></p>

Build the MyWizardDriver 

```
  C:/FW/edk2> Build
  C:/FW/edk2> Build Run
```

<b>Load</b> the UEFI Driver <br>
&nbsp;&nbsp;&nbsp;<font color="gray">`Shell> `</font>`fs0:`<br>
&nbsp;&nbsp;&nbsp;<font color="gray">`FS0:\> `&nbsp;</font>`load MyWizardDriver.efi`<br>
Observe the Buffer address is at `0x0587f010` as this slide example<br>


Note:

Same as slide




---?image=/assets/images/slides/Slide42.JPG
## Slide 42 @title[Lab 6 Verify Driver]
<p align="right">Lab 6: Verify Driver</p>
<br>
At the Shell prompt, type &nbsp;<font color="gray">`FS0:\> `&nbsp;</font>`drivers`<br>
<br>

Observe the handle is "`A9`" as this slide example <br>
Type: &nbsp;` mem  0x0587f010`<br>
Observe the buffer was filled with the "0x0042" <br>

Note:

Same as slide




---?image=/assets/images/slides/Slide43.JPG
## Slide 43 @title[Lab 6 Verify Unload]
<p align="right">Lab 6: Verify Unload</p>
<br>
At the Shell prompt, type &nbsp;<font color="gray">`FS0:\> `&nbsp;</font>`unload a9`<br>
<br>

Observe the DEBUG messages from the Unload<br><br>
Type `Drivers` again to verify<br>


Note:

Same as slide
        



---?image=/assets/images/slides/Slide44.JPG
## Slide 44 @title[Lab 6 Verify Unload]
<p align="right">Lab 6: Verify Unload</p>
<br>
At the Shell prompt, type &nbsp;<font color="gray">`FS0:\> `&nbsp;</font>`mem 0x0587f010  -b`<br>
<br>

Observe the buffer is now NOT filled <br>
<br>
<br>
<br>
<br>
<br>
Exit, type <font color="gray">`FS0:/ >`</font> `Reset`<br>

Note:

Same as slide
     
---?image=/assets/images/slides/Slide45.JPG
## Slide 45 @title[Additional Porting]
<p align="right">Additional Porting</span></p>  
<br>



Refer to the UEFI Drivers Writer’s Guide for more tips – <a href="https://legacy.gitbook.com/book/edk2-docs/edk-ii-uefi-driver-writer-s-guide/details">Pdf link</a></span>

Note:
Use the UEFI Driver Wizard to create a starting point for new drivers on EDK II


---  
## Slide 46 @title[Summary]
<BR>
<p align="center">Summary </p><br>
<ul>
 <li>Compile a UEFI driver template created fromUEFI Driver Wizard </li>
 <li>Test driver w/ Nt32 emulation using UEFI Shell 2.0</li>
 <li>Port code into the template driver </li>
</ul>

---?image=assets/images/gitpitch-audience.jpg
## Slide 47 @title[Questions]
<br>
![Questions](/assets/images/questions.JPG) 


---?image=assets/images/gitpitch-audience.jpg
## Slide 48 @title[Logo Slide]
<br><br><br>
![Logo Slide](/assets/images/TianocoreLogo.png =10x)


---
## Slide 50 @title[Acknowledgements]
