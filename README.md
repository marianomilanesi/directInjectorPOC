# directInjectorPOC

Small program written in C#, compatible with .NET >= v3.5 . Only x64. 

Created as a way to learn more about direct syscalls and their implementation in C#. 

The program uses direct syscalls to perform the shellcode allocating/injection and the remote thread creation. The only imports are GetSystemInfo, RtlGetVersion and VirtualProtectEx.

The shellcode can be easily generated using tools like donut (https://github.com/TheWover/donut/).

Current implementation allows downloading shellcode from a github repository using ssl sockets.

### Usage: 
The first step is to create a github repository and upload a shellcode.bin file containing the shellcode. Then replace the placeholders on line 15 with the corresponding information.

By default the program injects into "notepad" using the ALLOCWRITE write method. This can be easily modified by changing line 17 
```
Inject(sc, "notepad", osV, ALLOCWRITE);
```
can be changed to 
```
Inject(sc, "explorer", osV, OPENSEC);
```
to inject the shellcode into explorer.exe using the NtMapViewOfSection method. 
##### ToDo:

  - Implement more ways to write our shellcode in a remote process (process hollowing, dll hollowing, etc)
  - New execution methods (steal them from pinjectra :) )
  - Try to avoid the use of VirtualProtectEx when allocating our shellcode
  - Try catch everything just in case

##### Original POC:

  - https://github.com/fela15/directInjectorPOC

##### Links of interest:

  - https://ired.team/offensive-security/code-injection-process-injection/ntcreatesection-+-ntmapviewofsection-code-injection
  - https://ired.team/offensive-security/code-injection-process-injection/process-injection
  - https://github.com/TheWover/donut/
  - https://github.com/b4rtik/SharpMiniDump/
  - https://github.com/outflanknl/Dumpert (tool)  https://outflank.nl/blog/2019/06/19/red-team-tactics-combining-direct-system-calls-and-srdi-to-bypass-av-edr/ (blog)


