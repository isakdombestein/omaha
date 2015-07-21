## v1.3.28.1 - 2015-07-21 @54943000,96143042

### Changes
--------------------------------------------------------------------------------
  Standardize on Security Lite and deprecate WinCrypt. Now using SecurityLite instead of WinCrypt in the CryptoHash class.
--------------------------------------------------------------------------------
  Disable EtwTraceControllerTest.EnableDisable test.
  It hangs on Windows 7.
--------------------------------------------------------------------------------
  GoogleUpdateRecoveryTest.VerifyFileSignature* tests fail.
  SaveArguments.exe needs to be updated every 6 months.
  Now using the version 1.3.27.5 built on 5/1/2015.
--------------------------------------------------------------------------------
  Running Debug version of Omaha on Win 10 produces an assertion failed error OS_WINDOWS_UNKNOWN. The custom OS version detection code is dated. Moving Omaha code to using the Version Helper functions that shipped with the Windows 8.1 SDK.
--------------------------------------------------------------------------------
  Include the passed in install source for Omaha install ping as well.
--------------------------------------------------------------------------------
  Implement support for load shedding based on the priority of requests. The client sends a X-GoogleUpdate-Interactivity header to indicate whether the current request is foreground or background. A value of "fg" ("foreground") indicates foreground install or on-demand updates. "bg" ("background") indicates silent update traffic.
--------------------------------------------------------------------------------
  Fix Cohort attributes not being echoed to the update server in update checks. Also added unit tests for the Update Request as well as the Update Response.
--------------------------------------------------------------------------------
  Change the Test Omaha Exe Installer to correctly process installerdata. The code was not handling quoted paths correctly.
--------------------------------------------------------------------------------
  Support Retry-After header.
--------------------------------------------------------------------------------
  The ping event result for download metrics is incorrect in some cases.
  The idea here is that the ping event result corresponding to a download metrics should
  be consistent with the error member in the download metrics.
--------------------------------------------------------------------------------
  Add Installer Progress Reporting to Omaha. This change adds Installer Result API InstallerProgress Installer Progress Reporting to Omaha.
  Omaha now reads installation progress reported as a percentage from 0 to 100 in "InstallerProgress" under Google\\Update\\ClientState\\{AppID}, which allows the Omaha installation UI to show installation progress of any installer that writes the "InstallerProgress" value.
  Once this change is in, installers that write percentage progress to the "InstallerProgress" value as they progress through the installation will allow Omaha to automatically pick it up.
--------------------------------------------------------------------------------
  Check the custom HTTP header first, then check ETag if the former is not present or empty.
--------------------------------------------------------------------------------
  Implement an alt mechanism for ETag in CUP-ECDSA. There is now support for a "X-Cup-Server-Proof" custom header that we check first, and then fall back on the ETag header if the former is missing. The following formatting variations of the ETag/X-Cup-Server-Proof header are supported:
  * A Strong ETag formatted as S:H.
  * A Strong ETag formatted as "S:H".
  * A Weak ETag formatted as W/S:H.
  * A Weak ETag formatted as W/"S:H".
--------------------------------------------------------------------------------
  Add a X-HTTP-Attempts header to outgoing Omaha requests.
--------------------------------------------------------------------------------
  Adding IJobObserver2 handling for PerformOnDemand.
--------------------------------------------------------------------------------
  Installer progress for the OnDemand API. This change adds a new IJobObserver2 interface. IJobObserver2 provides a single method, OnInstalling2([in] int time_remaining_ms, [in] int pos), that gives installation progress when available. If an OnDemand client implements IJobObserver2, then the newer OnInstalling2() method will be called instead of IJobObserver::OnInstalling(). This will enable Chrome to show installation progress within the chrome://chrome page.
--------------------------------------------------------------------------------
  Add Chrome Installer Progress Reporting to Omaha. This change reads Installation progress reported in "InstallerExtraCode1" under Google\\Update\\ClientState\\{AppID}, and allows the Omaha installation UI to show installation progress of the Chrome installer. The Chrome installer writes the "InstallerExtraCode1" value as it progresses through the installation.
--------------------------------------------------------------------------------
  Implement cohort attributes.
--------------------------------------------------------------------------------
  Fix XP-compatibility for the VC 2013 build:
  * "GoogleUpdateSetup.exe is not a valid Win32 application": This is fixed by explicitly targetting Windows XP by setting the SUBSYSTEM to 5.01.
  * "The procedure entry point InitializeCriticalSectionEx could not be located in the dynamic link library KERNEL32.dll". ATL uses InitializeCriticalSectionEx unless we build with _ATL_XP_TARGETING.
--------------------------------------------------------------------------------
  Fix the GroupPolicyProxyDetector to work correctly on Domain and Non-Domain scenarios.
--------------------------------------------------------------------------------
  Fix UATest Group Policy related test cases to test Domain and Non-Domain scenarios.
--------------------------------------------------------------------------------
  Fix UpdateRequest and XmlParser Group Policy related test cases to test Domain and Non-Domain scenarios.
--------------------------------------------------------------------------------
  A SetupGoogleUpdateMachineTest unit test is broken. Changing vista_util::IsUACOn() to always reflect 'false' on platforms below Vista.
--------------------------------------------------------------------------------
  Fix Group-Policy-related test cases to test both Domain and Non-Domain scenarios.
--------------------------------------------------------------------------------
  Work around locked-down environments for CSIDL_PROGRAM_FILES and CSIDL_LOCAL_APPDATA. Using ::GetEnvironmentVariable when ::SHGetFolderPath fails.
--------------------------------------------------------------------------------
  Adding a new hammer command line switch --suppress_light_validation. This switch supresses WiX Linker ICE validation. Useful when building with a non-interactive account or a non-Admin account: http://goo.gl/UyDzeP.
--------------------------------------------------------------------------------
  Supress <LGHT0217: Error executing ICE action 'ICE01'> when building on the build server. ICE validation needs an interactive account or Admin privileges: http://goo.gl/UyDzeP.
--------------------------------------------------------------------------------
  Adding an UpdateDev override "EnrolledToDomain" that when set makes it look like the machine is enrolled to a domain.
--------------------------------------------------------------------------------
  Google Update Group Policy settings - change to work only for Domain Users.
--------------------------------------------------------------------------------
  Use OPT_LOG statements in the download manager
--------------------------------------------------------------------------------
  Download metrics for simple request don't include the error
  when a HTTP response is available and the response is an HTTP error.
--------------------------------------------------------------------------------
  BITS download metrics don't include the error in some cases
--------------------------------------------------------------------------------
  Have the OneClick control run GoogleUpdateWebPlugin.exe instead of GoogleUpdate.exe.
--------------------------------------------------------------------------------
  Fix time bombs in the experiment_labels_unittest
--------------------------------------------------------------------------------
  UI stuck on "Download complete.". STATE_READY_TO_INSTALL was being shown in the UI as "Download complete.".
--------------------------------------------------------------------------------
  crash_analyzer_checks.cc warning C6319: Use of the comma-operator in a tested expression causes the left argument to be ignored when it has no side-effects.
--------------------------------------------------------------------------------
  common\scheduled_task_utils.cc(369)warning C6216: Compiler-inserted cast between semantically different integral types:
--------------------------------------------------------------------------------
  popup_menu.cc(170)warning C6316: Incorrect operator: tested expression is constant and non-zero.
--------------------------------------------------------------------------------
  base\crash_if_specific_error.cc(29)warning C6230: Implicit cast between semantically different integer types:
--------------------------------------------------------------------------------
  net\simple_request.cc(728)warning C6246: Local declaration of 'response_headers' hides declaration of the same name in outer scope.
--------------------------------------------------------------------------------
  base\command_line_validator.cc(94)warning C6340: Mismatch on sign
--------------------------------------------------------------------------------
  base\clipboard.cc(48)warning C6387: 'copy_data' could be '0':
--------------------------------------------------------------------------------
  Fix static analysis warnings in proxy_auth.h
--------------------------------------------------------------------------------
  Disable some static analysis warnings.
  For everything, disable:
  '/wd28159', # Consider using 'GetTickCount64' instead of 'GetTickCount'.
  '/wd28204', # Inconsistent SAL annotations.
  '/wd28251', # Inconsistent SAL annotations.
  For unit tests:
  # Disable static analysis warnings.
  '/wd6326',  # Potential comparison of a constant with another constant.
--------------------------------------------------------------------------------
  utils.h(163)warning C6387: 'module' could be '0'
--------------------------------------------------------------------------------
  InstallHandoffUserTest fails for only Vista in 1.3.26.1.
--------------------------------------------------------------------------------
  Add better debugging support for optimized code via undocumented switch /d2Zi+. The size increase is minimal on the compile run (704 bytes). More information on this switch here: https://randomascii.wordpress.com/2013/09/11/debugging-optimized-codenew-in-visual-studio-2012/
--------------------------------------------------------------------------------
  Fix command line errors output for omaha_unittest.exe.
  This change avoids the --gunit_ --gtest_ differences between
  the internal and the open source versions of gTest.
--------------------------------------------------------------------------------
  Create a "prefer cacheable" flag in update requests.
--------------------------------------------------------------------------------
  Added more logging to group policy override related functions in ConfigManager.
--------------------------------------------------------------------------------
  Add a new policy to generated ADMs to select between secure and cacheable URLs for payloads.  Will require code support to implement.
--------------------------------------------------------------------------------
  Introduce hourly jitter for update checks.
--------------------------------------------------------------------------------
  Fix the unit test for OS upgrades to use the correct is_machine value.
--------------------------------------------------------------------------------
  Improve existing unit tests by adding the "machine" scenario.
  This is another mechanical change in preparation for
  introducing hourly jitter for update checks.
--------------------------------------------------------------------------------
  AutoRunOnOSUpgradeCommands AppCommands now run as fire-and-forget. 
--------------------------------------------------------------------------------
  Implement ping 14 component-updater style for Omaha.
--------------------------------------------------------------------------------
  Disable the test CoreTest.HasOSUpgraded
--------------------------------------------------------------------------------
  Reduce the number of retries for downloads from 3 to 1
--------------------------------------------------------------------------------
  Implement ping 14 component-updater style for Omaha
--------------------------------------------------------------------------------
  Add a unit test for OS upgrades which tests that the Core successfully runs corresponding AutoRunOnOSUpgrade AppCommands.
--------------------------------------------------------------------------------
  Removed DLL DELAYLOAD linkage flags so that the DLLs will be loaded at process start time (and thus eliminate the crash).
--------------------------------------------------------------------------------
  Crash in CComObject<AppCommandCompletionObserver> constructor. Going back to adding the ATL Module back in since we do create AppCommand COM objects, creating the Core on the heap and leaking the module. The Core now has a DeInit method that allows the QueueTimers to shut down.
--------------------------------------------------------------------------------
  Support sha-256 for download verification.
--------------------------------------------------------------------------------
  Disable SplashScreenTest.RenderResourceStrings_en, the test takes too long to run.
--------------------------------------------------------------------------------
  Remove duplicated uninstall ping.
--------------------------------------------------------------------------------
  Remove the assert which checks existence "network" reg key. The reg key is removed when we removed CUP RSA code.
--------------------------------------------------------------------------------
  Removed registry hive redirection which causes GetDir32() fail on XP. Instead, the tests now creates and cleans up specific registry keys.
--------------------------------------------------------------------------------
  Wait crash handler to exit before self-install.
  No extra code needed to shutdown the crash handler because ShutdownHandler in CrashHandler also observes the global shutdown event.
--------------------------------------------------------------------------------
  Compatibility manifest needs to be updated to make GetVersion(Ex) stop lying on Windows 10 Technical Preview.
--------------------------------------------------------------------------------
  Remove CUP RSA code.
--------------------------------------------------------------------------------
  Do not allow test cert in authenticode check.
--------------------------------------------------------------------------------
  Disabling ScheduledTaskUtilsTest.ScheduledTasksV2 test because we are seeing random failures with 0x80070005 on the UninstallScheduledTask call. 
--------------------------------------------------------------------------------
  Remove uilib since StaticEx and helpers are not needed anymore.
--------------------------------------------------------------------------------
  Use Wix version v3_8_1128
--------------------------------------------------------------------------------
  Close BITS job right after download.
--------------------------------------------------------------------------------
  Remove unused minicrt library.
--------------------------------------------------------------------------------
  Removes dependency of inttypes.h in favor of stdint.h.
  This gets rid of omaha/third_party/c99/.
--------------------------------------------------------------------------------
  Fix the constant shell version sent out in Update pings to be the installed version, not the version that is running the Update Setup code.
--------------------------------------------------------------------------------
  Pass MSI product guid to application installer. The application installer can use this to, for example, update entries in the Add/Remove Programs dialog.
--------------------------------------------------------------------------------
  Better fix for C4302 type truncation warning.
--------------------------------------------------------------------------------
  Changes required before switching to WTL 9.0.
--------------------------------------------------------------------------------
  Remove code that is no longer needed. introduced our own variant of ATL's statreg.h.
--------------------------------------------------------------------------------
  Ship the currently built version of the constant shell GoogleUpdate.exe instead of a checked-in version with the Omaha meta-installer. For updates of Omaha, we will only update the constant shell if the installed version is below kCompatibleMinimumOlderShellVersion (which is 1.3.21.103 as of 07/24/2014). This will ensure minimal firewall prompt concerns.
--------------------------------------------------------------------------------
  Update unit test for the minimum shell version 1.3.21.103.
--------------------------------------------------------------------------------
  Omaha 1.3.24.15 causes alerts of Comodo Internet Security's HIPS subsystem. Omaha updates itself by running the newer setup (GoogleUpdateSetup.exe) from %ProgramFiles%\Google\Update\Install\{UniqueDir}\GoogleUpdateSetup.exe. This setup in turn ends up deleting the %ProgramFiles%\Google\Update\Install directory including GoogleUpdateSetup.exe. Finally, GoogleUpdateSetup tries to cleanup the temp directory that it created under %ProgramFiles%\GUM*. The anti-virus program fails to validate the GoogleUpdateSetup.exe executable at this point because the underlying disk image has been deleted (or to be more accurate, moved via MoveFileEx, since the file is in use otherwise).
  The fix is to avoid deleting this directory at setup time, because the directory is cleaned up by the InstallManager at every Omaha update check.
--------------------------------------------------------------------------------
  [ASSERT][goopdate\install_manager.cc:76]. The install manager cleans up files in the Install directory on every initialization. It does this by first deleting the directory and contents, and then recreating it. This causes a problem if other monitoring or AV software has the Install directory in use. Instead, this fix only deletes files under the Install directory, because that is the original intent.
--------------------------------------------------------------------------------
  Restore Omaha Core and UA tasks on Update or Over-install. This change will reinstall the tasks every time Omaha installs or updates itself.
--------------------------------------------------------------------------------
  Bug fix: install time is missing from pings.
  The buggy code in the InstallManager captured the time after
  the app state transitions and builing the pings, therefore
  the install time was still missing.
--------------------------------------------------------------------------------
  Older constant shells do not have the manifest changes that were made to allow GetVersionEx to return Windows 8.1. This change fixes that by detecting Windows 8.1 and above without updating the constant shell.
--------------------------------------------------------------------------------
  Remove Omaha signature checks, including the associated debug pings
--------------------------------------------------------------------------------
  Download and install times must be reported in the completion ping in all cases.
--------------------------------------------------------------------------------
  Increase the installer complete wait time to 30 mins
--------------------------------------------------------------------------------
  For more resilient code, use SafeCStringAFormat() instead of directly calling CStringA::Format().
--------------------------------------------------------------------------------
  GoogleUpdateSetup.exe size increased by about 35KB in 1.3.24.7 from what it was in 1.3.23.9. Change 63760550 uses std::stringstream, which is responsible for the increase in the crash handler. This change makes use of ATL's CStringT instead.
--------------------------------------------------------------------------------
  Omaha crash uploader must use "guid" instead of "userid" standard field for uploads
--------------------------------------------------------------------------------
  Code red runs does not run after 1 day(or 2 days) but runs after one year. The root cause is trying to store a large millisecond value in an int, causing an overflow.
--------------------------------------------------------------------------------
  crash: omaha::WebServicesClient::http_trace()
--------------------------------------------------------------------------------
  Use lax criteria in updating "days-since" registry counters.
  This change makes the header name lookup case-sensitive and
  fixes the name of the header string literal to match the
  name the server is returning.
--------------------------------------------------------------------------------
  physmem must be rounded to the closest GB
--------------------------------------------------------------------------------
  Translations for the IDS_HW_NOT_SUPPORTED string.
--------------------------------------------------------------------------------
  Change the Code Red hostname to clients2.
--------------------------------------------------------------------------------
  Broken Unit Test: WinHttpAdapter.
  The code executed by the broken test was illegal to begin with. In some
  cases, it is possible for the underlying OS stack to not be initialized
  correctly at the time a WinHttpConnect call is made.
--------------------------------------------------------------------------------
  NewUI: On error, top of Help and Close buttons getting clipped.
--------------------------------------------------------------------------------
  Use the new GetIEPath() helper function in other places where the IE Path needs to be determined and currently use the registry directly.
--------------------------------------------------------------------------------
  Handle the error when the server responds with error-hwnotsupported.
--------------------------------------------------------------------------------
  Added IDS_HW_NOT_SUPPORTED.
--------------------------------------------------------------------------------
  Refactor the server response status strings to make it obvious
  where they are coming from. That is in preparation to adding
  a new status string.
--------------------------------------------------------------------------------
  Increase the limit for number of crashes uploaded / day
--------------------------------------------------------------------------------
  Remove checking the result of ResetCurrentStateKey().
--------------------------------------------------------------------------------
  Reorganize the crash handler into a more sensical structure. split crash worker specific methods out of utils into crash_worker.cc
--------------------------------------------------------------------------------
  for Win8: IE is not opening with toolbar when click on restart now button. On Win8 64-bit the Wow6432 node has ielowutil.exe instead of iexplore.exe. The change is to use iexplore.exe
  from the same directory containing ielowutil.exe.
--------------------------------------------------------------------------------
  Sandbox MinidumpWriteDump, include user stream information from the crash analyzer in minidumps
--------------------------------------------------------------------------------
  ::GetThreadId API not available on Windows XP, causes build break.
--------------------------------------------------------------------------------
  Possible race condition in AppCommandCompletionObserver. The workaround here is to leak the ATL Modules. While this approach is not generally recommended, ATL modules are meant to live for the lifetime of the process, and this change makes it so. Because of the hybrid modes that Omaha runs under and because ATL relies on global structures, we need multiple modules and cannot statically allocate.
--------------------------------------------------------------------------------
  Make https the prefered protocol for update checks
  Not including the downloads, Omaha network traffic has been moved to use HTTPS always,
  with two exceptions. The update checks and pings fallback to using HTTP if HTTPS fails.
--------------------------------------------------------------------------------
  GUpdate and GUpdateM services stuck in "Service starting" instead of "Service running".
--------------------------------------------------------------------------------
  Security: (MODERATE risk) Add SSL to code red for defense in depth
--------------------------------------------------------------------------------
  Fix broken xml parser unit tests.
--------------------------------------------------------------------------------
  Allow config rule tests for HW platform information, such as SSE2 support.
--------------------------------------------------------------------------------
  Register a ETW provider also triggers callback if EnableTrace() is called before that.
--------------------------------------------------------------------------------
  Fix crashes in the crash handler.
  Disable the nt functions analyzer check. It creates too many false positives anyway.
--------------------------------------------------------------------------------
  BufferToPrintableString can crash when built under VS2010 in dbg.
--------------------------------------------------------------------------------
  Check request/response cookie existance only for RSA CUP. Duplicated tests for RSA CUP and ECDSA CUP.
--------------------------------------------------------------------------------
  Duplicate the reg values necessary for the test to pass on Vista and later.
--------------------------------------------------------------------------------
  Add the capability to embed user data streams with additional information about a crash analysis result into a minidump
  Add additional information for the postive case in the checks.
--------------------------------------------------------------------------------
  Move Chrome files to make organization compliant with third_party rules
--------------------------------------------------------------------------------
  Add support for detecting processor features.
--------------------------------------------------------------------------------
  Reuse Chromium CPU class for processor features including SSE2 support. 
  These are the original files from Chromium.
--------------------------------------------------------------------------------
  Resolved UT VerifyFileSignature_NonGoogleSignature failure.
  Issues resolved:
  1) Picked the right file for signature check on Vista and later.
  2) Expand SYSTEM macro before checking file existance.
  3) Corrected the expected error code.
--------------------------------------------------------------------------------
  Change extractor_unittest to use the untagged GoogleUpdateSetup_repair.exe instead of GoogleUpdateSetup.exe, because the latter is tagged with the omaha signature.
--------------------------------------------------------------------------------
  Fix file length check to be less onerous.
--------------------------------------------------------------------------------
  Change install ping attribute "install_day" to "installdate".
--------------------------------------------------------------------------------
  Self signing cert has expired and UTs are failing.
--------------------------------------------------------------------------------
  Fixed the build break when building 64-bit performondemand.exe.
--------------------------------------------------------------------------------
  Create 64-bit version of performondemand.exe for test.
--------------------------------------------------------------------------------
  crash_dump_util's CreateCrashHandlerProcess() misuses System::StartProcessWithEnvironment().
--------------------------------------------------------------------------------
  Closes minidump file handle before do crash reporting to avoid file open error.
--------------------------------------------------------------------------------
  Added 64-bit proxy into meta-installer.
--------------------------------------------------------------------------------
  Make copy of build env to avoid unwanted changes made by the building process.
--------------------------------------------------------------------------------
  Make build script generates Omaha IDL proxy for 64-bit platform as well.
--------------------------------------------------------------------------------
  Update pin list for code signing.
  This defines the sha1 cert that replaced the sha256 cert, which was briefly in use for 1 day. It updates the unit test to check for old and new signatures.
--------------------------------------------------------------------------------
  Update the code signing certificate hash pin list to include the new Chrome code signing certificate.
  Once we have a sample code signed with the new certs, UT must be updated to include the new file.
  We will keep the old pin while transitioning.
--------------------------------------------------------------------------------
  Do not adjust installage to first day of week for -1.
--------------------------------------------------------------------------------
  Now that CUP-ECDSA is enabled on prod servers, make CUP-ECDSA on by default.
--------------------------------------------------------------------------------
  Incorrect format string in log statement could cause exception.
--------------------------------------------------------------------------------
  Add UpdateDev regkeys to disable CUP and enable CUP-ECDSA.
--------------------------------------------------------------------------------
  Add an ASN.1 DER decoder that is capable of decoding complete ECDSA signatures.  Prep work for accepting an ASN.1 signature instead of discrete (R,S) integers.
  The motivation for this change is that the Chrome libraries, and pretty much all other libraries in the Google codebase, work in terms of complete signatures instead of (R,S).  If we're adding CUP-ECDSA to other clients besides the main Omaha Client, it makes sense to pick a single signature type that works for the majority of them.
--------------------------------------------------------------------------------
  Ensure that delays aren't moved to a negative amount as a result of jitter.
--------------------------------------------------------------------------------
  Remove temporary registry value that saves xdaynum. Set the value as a property of app.
--------------------------------------------------------------------------------
  Report install age and active/roll call days based on the daynum in server's response.
--------------------------------------------------------------------------------
  Changing the placement of the Error Text to match with the original UX spec. This requires more changes to strings that are too long. since these are my own ad-hoc changes, please carefully review the string changes to concur that the new strings make sense.
--------------------------------------------------------------------------------
  Downsize and move the Help button, and integrate new translations.
--------------------------------------------------------------------------------
  Broken Unit Test: CoreUtilsTest. Also addresses Make Omaha compatible with Windows 8.x.
--------------------------------------------------------------------------------
  Fixing unit test failures. Also fixing a bug in the formatting of some resource strings.
--------------------------------------------------------------------------------
  Fix the splash screen unit test v2. This was due to my incorrect assumption that the animation control would not hold onto the resource handle.
--------------------------------------------------------------------------------
  Fix broken unit test. Explicitly loading goopdate.dll now for the UI resources.
--------------------------------------------------------------------------------
  Enclosed the Animate_* calls with VERIFY1 for completeness.
--------------------------------------------------------------------------------
  Less verbose strings for the Omaha UI.
--------------------------------------------------------------------------------
  Omaha takes up too much disk space after Omaha Visual Refresh. Moving the big non-localized resources over to goopdate.dll to fix this issue.
--------------------------------------------------------------------------------
  Implement sandbox for omaha crash handler.
  This adds the plumbing to deal with all the needed files and handles by opening handles ahead of time.
  It then creates seperate worker process to perform the crash dump and (after opening all needed handles) locks down the process by setting the untrusted label on the processes access token.
--------------------------------------------------------------------------------
  Bits request falls back to direct access when GetProxyForUrl() returns failure.
--------------------------------------------------------------------------------
  Avoid to kill process not owned by current user.
  Increase wait time out during process killing to avoid time out error.
--------------------------------------------------------------------------------
  Broken Unit Test: GetBundleCompletionMessageTest.
--------------------------------------------------------------------------------
  Omaha binaries built with VC2010 don't have debugging information.
--------------------------------------------------------------------------------
  Do not expand tag length as signed integer.
--------------------------------------------------------------------------------
  Omaha binaries built with VC2010 don't have debugging information.
--------------------------------------------------------------------------------
  Update MSI custom action DLLs to comply with server side tag format.
--------------------------------------------------------------------------------
  Change the build version on trunk so that is always higher than milestone branch builds.
  Omaha migrates to a Chrome-model where the milestone is encoded as the build number in the major.minor.build.patch scheme.
  For example, 1.3.22.1, 1.3.22.3, 1.3.22.5 mean M22 builds of Omaha, cut on a release branch.
  1.3.23.1 means an M23 build, and so on.
--------------------------------------------------------------------------------
  Make MSI tag format to comply with what server has.
--------------------------------------------------------------------------------
  Empty "Offline" directories created for each Omaha install.
--------------------------------------------------------------------------------
  Assert when installing using the Avast build. The CurrentState key was not created, so the write was failing. Creating/resetting the CurrentState key in STATE_INIT now, and always Creating the key before writing.
--------------------------------------------------------------------------------
  Support reading tag from MSI business installer.
--------------------------------------------------------------------------------
  Define API for Install progress.
--------------------------------------------------------------------------------
  Omaha download in Avast happen at background priority and take longer than needed. Now all installs run at high priority. Even if the install is silent. Most install use-cases require the install to complete quickly. For instance, Avast launching the Omaha metainstaller with /silent while showing their own UI. Updates continue to run at low priority when not interactive (the majority use-case).
--------------------------------------------------------------------------------
  Resize the Show me help for this issue" button to be large enough to fit text for de, ro, nl.
--------------------------------------------------------------------------------
  Ensure module handles are closed after debugging the process.
--------------------------------------------------------------------------------
  Make install result text more compact to the left.
--------------------------------------------------------------------------------
  Fix static_assert so that it does not conflict with c++11 static_assert.
--------------------------------------------------------------------------------
  Branding change to use the Color Chrome logo instead of the monochrome logo. Also changing the layout of some controls to better center the progress bar, information/error text, and the new logo.
--------------------------------------------------------------------------------
  Fix issue with window jumping around if the mouse is moved with the left button down from outside the title bar and then into it keeping the mouse button down. The title bar now only moves the underlying window if it has the mouse capture.
--------------------------------------------------------------------------------
  Fixed the expectations for http_trace(). This function is called different times in opt and dbg modes.
--------------------------------------------------------------------------------
  Add a usagestat for skipping BITS due to machine case.
--------------------------------------------------------------------------------
  Add unit tests that stress ClientStateMedium experiment label merging.
--------------------------------------------------------------------------------
  When a update for an app is skipped due to Group Policy, emit that to optlog instead of corelog.
--------------------------------------------------------------------------------
  The event log source for Omaha crashes event 2 shows as Update2.
--------------------------------------------------------------------------------
  Turn on crash analysis for non-system crash handlers.
--------------------------------------------------------------------------------
  Adjust the height of the installer state text box to accomodate longer messages and product names. Also adjusted a couple of other boxes that are not used currently but may be used in the future.
--------------------------------------------------------------------------------
  Fixed the expiration date for the Chrome code signing certificate.
--------------------------------------------------------------------------------
  Adjusting the dimensions of the Cancel and the YesNo dialog buttons to look more like the spec.
--------------------------------------------------------------------------------
  Changes to allow the UI to work consistently in XP. Without these changes, the XP UI scaled incorrectly. 
--------------------------------------------------------------------------------
  Marquee progress bar for showing indeterminate progress during all phases other than download. Removing throbber and showing the Chrome icon during most installation phases. Color correction for the caption button highlight.
--------------------------------------------------------------------------------
  Broken Unit Test: AppUtilTest.
  The issue here is that GetModuleFileName is unreliable under WoW64.
--------------------------------------------------------------------------------
  SimpleRequestTest.HttpGetProxy* tests are broken.
  This changelist changes the behavior of the SimpleRequest so that a failure to detect a proxy is not considered a failure, instead, the code falls back to using direct access.
--------------------------------------------------------------------------------
  Positioning and sizing more of the controls to account for the changed layout.
--------------------------------------------------------------------------------
  Rendering changes to have the Caption Buttons match the UX spec.
--------------------------------------------------------------------------------
  Read from ClientStateMedium when scanning experiment labels.
--------------------------------------------------------------------------------
  Sizing the caption buttons a bit bigger. Creating brushes once instead of during each paint operation.
--------------------------------------------------------------------------------
  Reworking progress bar painting logic to better match the revised UX spec.
--------------------------------------------------------------------------------
  Handle errors when calling [Web]SafeBase64Unescape functions
--------------------------------------------------------------------------------
  Thread pool might time out during cancel and destruction of the Worker.
  Raise an exception when timeout occurs so at least, the code crashes in a deterministic way.
--------------------------------------------------------------------------------
  Use rand_s where possible.
--------------------------------------------------------------------------------
  Removing the caption buttons from the "Prefers" Yes/No dialog to make it uniform with the Cancel dialog. Fixing bug with the completion error image not showing up in certain cases.
--------------------------------------------------------------------------------
  Have a random delay of [0,60) seconds before an update check is made in the case of automatic silent update of all apps.
--------------------------------------------------------------------------------
  * due to sign extending and messing up the bit pattern when the default char type changes from unsigned to signed char.
  * Remove unused version 4_43 of the lzma library.
--------------------------------------------------------------------------------
  Fixed error_illustration.bmp replacing the background to 0xfbfbfb using gimp. Reverted chrome.ico to version 1, version 2 does not look as good. Imported translations for string id 822209109398822588 "Show me help for this issue" from transconsole.
--------------------------------------------------------------------------------
  Updated comment for AtlAssertTest.
--------------------------------------------------------------------------------
  Changes to make the code compatible with VS2010. It's minor tweaks to the code, good for any toolchain.
--------------------------------------------------------------------------------
  Dynamically sizing caption buttons now. Adjusting caption button colors to match spec.
--------------------------------------------------------------------------------
  Flat buttons for the new UI.
--------------------------------------------------------------------------------
  Show the Chrome icon when downloading the Chrome app. For now, this is implemented as a resource bundled with goopdate.dll and special-cased for the Chrome AppId.
--------------------------------------------------------------------------------
  Fix out of bounds read in crash analyzer
--------------------------------------------------------------------------------
  Reposition controls to match with UX requirements. Convert Help link to work like a button now.
--------------------------------------------------------------------------------
  Add the ability to set serverInstallDataIndex via IAppWeb.
--------------------------------------------------------------------------------
  Fix a unit test failure. The expectation is no longer true since now client always sends the first UID as Old-Uid.
--------------------------------------------------------------------------------
  Add UID history info to X-Old-Uid header (uid age, number of rotations etc.)
--------------------------------------------------------------------------------
  Add Windows 8.1 to the list of versions in SystemInfo.
--------------------------------------------------------------------------------
  Use relative paths when constructing paths within the ActiveX control so the control works under an AppContainer EPM environment.
--------------------------------------------------------------------------------
  Truncate installage to (now-daystart). Use that value for installage report only. For legacy apps, the value might be missing and will fall back to original installage in that case.
--------------------------------------------------------------------------------
  Report user cancel at which state, how long since update is available/since download start when cancellation happens.
--------------------------------------------------------------------------------
  Register OneClick and Update3Web controls as CATID_AppContainerCompatible for compatibility with Enhanced Protected Mode on Windows 8.x.
--------------------------------------------------------------------------------
  Report which url served installer download.
--------------------------------------------------------------------------------
  Adding in plumbing for showing App Icon. Updating dialog templates to use Segoe UI.
--------------------------------------------------------------------------------
  Take out flags added in DbgHelp 6.1
--------------------------------------------------------------------------------
  Use correct string arguments for log statement in crash handler util.
--------------------------------------------------------------------------------
  If we're impersonating (as in the machine /ua case) when creating a bundle, revert to self when creating a global mutex.
  Also, don't let an unexpected failure to create that global mutex DOS Omaha.
--------------------------------------------------------------------------------
  Update the signing date of the code red test file to avoid unit test failures.
--------------------------------------------------------------------------------
  install priority
--------------------------------------------------------------------------------
  Turn on the crash analyzer.
  Add a crash analysis key to the custom info map to get the result server side.
  Add additional info to crash dumps that trigger an analysis result.
--------------------------------------------------------------------------------
  Add install time to the ping 2s.
--------------------------------------------------------------------------------
  Expose a global Win32 event that's created when an installed app is added to a bundle, and deleted when the bundle is destroyed.  If the event exists prior to the app's creation, it cannot be added to the bundle.  This will be used to synchronize with external (in-process) product updaters.
--------------------------------------------------------------------------------
  Add a cache for memory segments read from the debugee. This avoids repeatedly calling ReadProcessMemory on the same segment
--------------------------------------------------------------------------------
  Add more time metrics: app update check time and installation time.
--------------------------------------------------------------------------------
  Hide the throbber on completion.
--------------------------------------------------------------------------------
  Control whether the throbber is shown/hidden based on marquee mode.
--------------------------------------------------------------------------------
  Have StaticEx align text based on the window style, instead of hardcoding left-alignment.
--------------------------------------------------------------------------------
  Reduce flicker by only updating the control if the text has changed. There are too many OnDownloading notifications, and with the increased font size, this is very noticeable.
--------------------------------------------------------------------------------
  Fix issue with throbber not showing when "Waiting to download". Turns out that this is because we are at the downloading stage (OnDownloading is being called), but showing a "Waiting to download" message instead. Fixing to show the correct message.
--------------------------------------------------------------------------------
  Add tests for the rest of the crash analyzer cases.
--------------------------------------------------------------------------------
  Move download time from ping 1 (download complete) to 2 (install complete) or 3 (update complete).
--------------------------------------------------------------------------------
  Integrate translations for the caption button tooltips.
--------------------------------------------------------------------------------
  Add several initial unit tests for the crash analyzer. Additionally fix a few bugs I found on the way.
  - misuse of scoped_array in a few places
  - a couple of places were using different const instances of maps for the begin() and end() of loops leading to badness
  - the initial thread of a process does not generate a create thread debug event (it is instead passed in the create process event) so I now add that thread to the thread map.
--------------------------------------------------------------------------------
  Creates a separate process with same privileges as the crashed process to handle the crash.
--------------------------------------------------------------------------------
  Make customization unit tests can be run from any directory so that run_uni_tests.py script can run properly.
--------------------------------------------------------------------------------
  Bigger dialog templates and fonts. Throbber instead of marquee progress bar for initialization and installation phases.
--------------------------------------------------------------------------------
  Make custom info population before dump generation as an optional operation.
--------------------------------------------------------------------------------
  Make the OneClick control more resilient to command injection attacks.
--------------------------------------------------------------------------------
  Update help URL to format changes
--------------------------------------------------------------------------------
  when escaping strings which prevents some characters from being escaped.
--------------------------------------------------------------------------------
  Unit test ProcessTest.GetImagePath because the image path returned by two different methods could differ in case, esp. for the drive letter (c: vs. C:).
--------------------------------------------------------------------------------
  Test AppUtilTest.GetModule* fails when AppVerifier is turned on with certain flags. This because the tests try to find module 'kernel32.dll' by looking for ::LoadLibrary() which could be redefined by AppVerifier. Switch to a function that is not redefined by AppVerifier.
--------------------------------------------------------------------------------
  move the wild stack pointer check to the end. Chrome uses the same check to determine whether to trigger a crash report when terminate process is called. In cases where the report was only generated because of this condition we are already pretty sure something nasty is happening and can gain additional context by running the other checks first.
--------------------------------------------------------------------------------
  Adds check for jmp->call->pop sequence of instructions around the crashing address.
  THis is indicative of shellcode that is trying to determine the address where it is located.
--------------------------------------------------------------------------------
  Define a new element in the xml protocol for unstrusted data.
  Untrusted data in a tagged meta-installer should be included in update request.
--------------------------------------------------------------------------------
  Add in localization for the caption button tooltips.
--------------------------------------------------------------------------------
  Add utility functions for reading exception information out of the crashing process
  Add check for access violations on addresses commonly used to defeat aslr
--------------------------------------------------------------------------------
  Adding untrusteddata in update request.
--------------------------------------------------------------------------------
  Add check for spray patterns which are useful for pivoting a vtable into shellcode.
--------------------------------------------------------------------------------
  Restructure the CrashAnalyzer class to split analysis into several stages.
--------------------------------------------------------------------------------
  Get rid of the module name from ModuleInfo because
    1. The debugging APIs do not reliably provide this information anyway
    2. The names are not really required for any of the planned checks
    3. This information is already available in the crash dumps (so we can get it server side if we decide we need it)
    4. This code was convoluted and wouldn't work the majority of the time anyway
  Add the base image to the module list
  Add a check for executable mapping which contain PEs that have been loaded without entries in the module list (common late stage malware pattern)
--------------------------------------------------------------------------------
  Restore IApp to its original interface and introduce IApp2.
--------------------------------------------------------------------------------
  Fix a bug with FillRgn and RTL/mirroring. Fix a bug with the marquee running from a non-min position.
--------------------------------------------------------------------------------
  Add check to scan each thread's stack for pointers to low level functions commonly used in ROP chains
--------------------------------------------------------------------------------
  Change LPVOID to BYTE* to make pointer math less convoluted.
  Add Some utility functions to the crash analyzer which various checks will use.
  Add a check for stack pointers which point outside a thread's actual stack segment.
  This indicates that either a the stack pointer itself is corrupt or that a stack
  pivot has occurred and stack is now attacker controlled.
--------------------------------------------------------------------------------
  Fixes an issue with the Marquee mode not moving the progress bar all the way to the right.
--------------------------------------------------------------------------------
  Restructure CrashAnalyzer and add a wrapper class for the individual checks.
  This change also adds one very simple check to demonstrate how this will work.
--------------------------------------------------------------------------------
  Custom Progress Bar Control class for the Omaha UI refresh.
--------------------------------------------------------------------------------
  This change adds functionality for hover and click effects on the caption buttons. This change also adds in a bigger delay before the tooltips for the caption buttons are shown, similar to how Windows does it.
--------------------------------------------------------------------------------
  Fix minimize/restore issues with the owner draw title bar. The popup title bar paints too quickly when the main window is being restored resulting in a floating title bar for a split-second. To fix this, I am changing the design to have the title bar be a child window of the dialog.
--------------------------------------------------------------------------------
  Add initial stub for a client side crash analyzer to flag crashes that look like failed exploit attempts.
--------------------------------------------------------------------------------
  * Enable all dialogs for the new look UI.
  * Functionality for dynamically enabling/disabling caption buttons.
  * Functionality for custom dialog backgrounds.
--------------------------------------------------------------------------------
  explicit client-regulated counting flag.
--------------------------------------------------------------------------------
  Build elliptic cryptography code.
  Fix more broken build issues.
--------------------------------------------------------------------------------
  Some Base classes for the new Omaha UI. Owner draw Title Bar and Buttons.
--------------------------------------------------------------------------------
  Build elliptic cryptography code.
  Added missing unit test file.
--------------------------------------------------------------------------------
  Build elliptic cryptography code.
  * the string code comes almost as-is from google3 plus some type changes to deal with warnings regarding conversion from size_t to int.
  * the ECDSA unit test depends on openssl and it is not part of the unit tests at the moment.
  * the include directives are somehow inconsistent since the original and most of the code integrated before is including just the file name, without any relative path to the root of the project.
--------------------------------------------------------------------------------
  Stop setting the IsMachine environment variable globally.
  Instead, set IsMachine on the environment block, when calling installers.
--------------------------------------------------------------------------------
  [ASSERT][base\system.cc:509][env_block]
--------------------------------------------------------------------------------
  chrome will not update behind a proxy.
  * Log the user account that the network stack is authenticating with.
--------------------------------------------------------------------------------
  Disable frame pointer optimization.
--------------------------------------------------------------------------------
  server and client enums for install sources are not in sync.
--------------------------------------------------------------------------------
  Allow clients to read the text output from application commands.
  Define a new AppCommand property "CaptureOutput". If true, the client can retrieve the STDOUT of the launched process. There is a limit of 64KB.
--------------------------------------------------------------------------------
  Add support for UpdateDev\CrashReportUrl override to crash uploading.  Add an UpdateDev\MaxCrashUploadsPerDay override as well.
--------------------------------------------------------------------------------
  Define a registry flag that can be used to disable app command executable verification for testing purposes.
--------------------------------------------------------------------------------
  Define a flag that allows system-level app commands to execute as the current user rather than as system.
  This resolves http://crbug.com/160293 (although Chrome setup will have to set the 'RunAsUser' flag too).
--------------------------------------------------------------------------------
  Refactoring code in crash_utils.cc to use EnvironmentBlockModifier.
--------------------------------------------------------------------------------
  Implementing "untrusted data" tag in Omaha.
  This is work-in progress to Implement "untrusted data" tag in Omaha.
  The "DATA" string is passed to GoogleSetup.exe by existing code
  where it is passed as environment variable to the {PRODUCT} installer.
  Validation from GoogleSetup.exe for character set and length:
  - Max length is 4096.
  - Only printable characters (ASCII [32,126]) is allowed, after unescaping.
--------------------------------------------------------------------------------
  - Assert InitializeUserIdLock in goopdate_utils.cc Line 1610 when /install or /ondemand is run.
--------------------------------------------------------------------------------
  Remove the CUP optimization of reusing credential for multiple requests.
--------------------------------------------------------------------------------
  Improve flaky SystemMonitor unit test. The SystemMonitor has a race condition when creating and deleting keys and values quickly. Changes can be missed. This behavior is by design and it can't be easily fixed. I incresed the time interval between successive tests. The rest of the refactoring is not essential.
--------------------------------------------------------------------------------
  Use the HTTPS url to upload crash reports.
--------------------------------------------------------------------------------
  When experiment labels are specified via a tag for either an app or Omaha, merge them with existing labels in the Registry instead of overwriting entirely.  (If the Registry labels appear to be corrupt, discard them and overwrite.)