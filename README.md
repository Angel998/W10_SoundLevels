# W10_SoundLevels


### A simple way to control the volume of speaker levels in C ++

![](https://i.imgur.com/0C5ujkJ.png)

[BaseCode from MSDN Forum](https://social.msdn.microsoft.com/Forums/windowsdesktop/en-US/9741bae1-c330-4802-9860-2fd202dba797/enumeration-of-available-levels-for-a-specific-installed-sound-card?forum=windowspro-audiodevelopment)
=============

CheckPoints
=============

### Get the local ID for volume level  - Line 133
                
----

```c++
    hr = pPart->GetLocalId(&pwszPartLocalId);
	if (FAILED(hr)) {
		printf("Could not get part local id: hr = 0x%08x", hr);
		return hr;
	}
	if (pwszPartLocalId == NULL) {
		pwszPartLocalId = 0;
	}

	printf("Part name: %ws, Part LocalId: %d \n", *pwszPartName ? pwszPartName : L"(Unnamed)", pwszPartLocalId); // <------ Get your ID
```

### Check the Local Id - Line 159
                
----
```c++
 is_audio_in = pwszPartLocalId == 131074;

hr = DisplayVolume(pVolume, iTabLevel);
if (FAILED(hr)) {
			printf("DisplayVolume failed: hr = 0x%08x", hr);
			pVolume->Release();
			return hr;
}

pVolume->Release();
is_audio_in = false;
```

### Handle volume level - Line 273
                
----
```c++
if (is_audio_in) {
			hr = pVolume->SetLevel(n, fMinLevelDB, NULL); // To 0
			//hr = pVolume->SetLevel(n, fMaxLevelDB, NULL); // To 100
			if (FAILED(hr)) {
				printf("Error when tried to set Mic-in volume");
			}
}
```
