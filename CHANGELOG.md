# DriveScope changelog

Versions follow MAJOR.MINOR.PATCH. The version lives in the `VERSION` file; `build.sh` writes it into the
exe (Properties › Details), the manifest and the app footer, together with a build date/time stamp.

## 1.18.1 — 2026-11-11
- First version published on GitHub: updates now come from github.com/Dialsoft/drivescope-releases.
- The updater also accepts the checksum written directly in latest.json (as Dialsoft's other programs publish it).

## 1.18.0 — 2026-11-02
- **New: automatic updates from GitHub.** DriveScope checks github.com/Dialsoft/drivescope-releases a few
  seconds after it starts and every 6 hours. The header button shows "✓ Up to date", "⬆ Update to x.y.z" or
  "⚠ Update check failed" (click to check now); when a new version exists a banner shows what's new with an
  **Install now** button, and an option to install updates automatically whenever DriveScope is idle. Updates are
  verified against the published SHA-256 checksum, never install while a test or erase is running, and DriveScope
  restarts itself (the page reconnects). Only the program is published – the source code stays private.
- **New: 📣 Share** – tell someone about DriveScope by email (mail app, Gmail, Outlook web), Facebook Messenger,
  WhatsApp, Microsoft Teams, text message (Phone Link), a Facebook / LinkedIn / X post, or a QR code. The message
  is editable, greets the person by name and signs with your name (remembered).

## 1.17.0 — 2026-10-30
- **New: memory type (NAND) of SSDs** – SLC / MLC / TLC / QLC, with bits per cell, the typical P/E-cycle range
  (SLC 50,000–100,000 · MLC 3,000–10,000 · TLC 1,000–3,000 · QLC 100–1,000) and what it means, plus the drive's
  own wear figure and how many times its capacity has been written. Drives don't report their memory type, so it
  comes from the makers' specifications – the model list now also covers common laptop OEM drives (WD PC SN-series,
  Samsung PM9xx, SK hynix BC/PC, Micron 2xxx, Kioxia BG/XG, Team MP33, Sabrent Rocket/Rocket Q…). Unknown models
  get an estimate from the sustained-write test (QLC slows down far more once its cache is full). Hover for the
  full SLC→PLC table. The memory type is printed on the label.
- **Fixed:** model patterns for SK hynix P41/P31 also matched Kingston OEM part numbers ("OM8PGP41…"), giving those
  drives the wrong rated speed. Samsung 850 PRO / 860 PRO are now correctly MLC (were listed as TLC).

## 1.16.0 — 2026-10-23
- **New: TRIM status always visible.** The header shows **TRIM ✔ on** (checked with Windows every minute and
  after every job) – or a red **⚠ TRIM is OFF** with a **Turn TRIM on** button if anything ever left it off.
- **New: "TRIM this drive now"** (Tools). Runs Windows' own retrim on the drive's volumes – the same step
  "Optimize Drives" does weekly: it tells the SSD which space is free, changes no files and causes no wear.
  Shows whether Windows TRIM is on, whether the drive supports TRIM, which volumes are trimmed and the result per
  volume (with a plain message when Windows can't, e.g. through some USB docks). Allowed on the Windows drive too,
  since it changes nothing on it. Limited to 15 minutes per volume.

## 1.15.2 — 2026-10-23
- **New: "Skip TRIM during the format"** in the Format / Create / Prepare for sale dialog – on by default for
  drives in USB docks. A quick format also TRIMs the whole drive; many docks (and some drives) take too long
  with that, Windows resets the device and the drive disconnects mid-format. DriveScope switches Windows' TRIM
  off only for the format and always switches it back on afterwards – also if the format fails, and at the next
  start if DriveScope was closed in the middle (the old setting is kept in a note file until it's restored).

## 1.15.1 — 2026-10-23
- **Fixed: "Invalid Parameter" during the quick format** (Prepare for sale / Create / Format). Windows' storage
  service sometimes refuses to format a partition it has only just created. DriveScope now waits and tries
  again, and if Windows still refuses, formats with Windows' classic FORMAT command instead (exFAT / NTFS /
  FAT32, quick, with the volume name). An empty volume name is no longer passed to Windows (that alone can cause
  "Invalid Parameter"). If everything fails, the message explains what to try instead of showing Windows'
  "Activity ID" code.

## 1.15.0 — 2026-10-23
- **New: automatic volume name.** Format / Create partition / Prepare for sale now fill in the volume label
  automatically from a name (default **DriveScope**) plus today's date, shortened to fit Windows' rules:
  NTFS (up to 32 characters) → "DriveScope10-23-26"; exFAT/FAT32 (up to 11) → "Drive102326" (FAT32 always in
  capitals). The name and the "add today's date" switch are in the dialog and are remembered; the label itself
  can still be typed over (characters Windows refuses are filtered out as you type), with a link back to the
  automatic name.

## 1.14.0 — 2026-10-23
- **New: "Connected via" line** at the top of the Test panel, saying plainly where the drive is plugged in:
  🖥 **Motherboard M.2 / PCIe slot** or **Motherboard SATA port** (with the PCIe/SATA link speed), or
  🔌 **USB dock / adapter** (with the dock chip and USB speed, and a note that docks limit speed and can block
  some tools), or 🔌 **USB port** for flash drives and card readers. The drive list shows the same
  (🖥 M.2 slot / 🖥 SATA port / 🔌 USB dock).
- **New: "Quick test + print label" button** next to Quick test. It runs the quick test and prints the label on
  the Brother QL as soon as it finishes – even if you've switched to another drive meanwhile. If the test is
  cancelled or doesn't finish, nothing is printed. Asks you to choose the printer first if none is set up.

## 1.13.4 — 2026-10-19
- **Form factor can be corrected in one click** on the drive details (M.2 2280/2242 SATA B+M key, M.2 NVMe M key,
  mSATA, 2.5" SATA). It is saved for that drive (by serial number) and used on the label. Unbranded SATA drives
  that report "2.5"" get a hint to check the card: two notches = M.2 SATA – many cheap drives copy this field
  from a template and report it wrong.

## 1.13.3 — 2026-10-19
- **Better M.2 (NGFF) reporting.** M.2 SATA drives that don't fill in the form-factor field were shown as
  2.5" SATA. They are now also recognised by model number (Crucial "…SSD4", WD Blue "…B0B", Kingston
  "SA400M8…", Samsung "MZ-N…", "M.2" in the name) and by the enclosure (a SATA drive behind a Realtek
  RTL9210/9220 bridge is always M.2). The form factor now names the card's keying: **M.2 SATA (B+M key)** – two
  notches; **M.2 NVMe (M key)** – one notch; x2 NVMe cards as "B+M or M key".

## 1.13.2 — 2026-10-19
- **Fixed: genuine drives flagged as counterfeit because a part number was read as the capacity.**
  "TEAM TM8FP6256G" was read as 6,256 GB (6.26 TB) instead of 256 GB, so a genuine 256 GB drive failed with
  "Model name says 6.26 TB". A capacity is now only taken from a number that stands on its own ("500GB",
  "-512G"); when it is glued to a part number ("SA400S37240G", "TM8FP6256G") only a standard size at the end
  counts (240 GB, 256 GB). Names without a clear capacity make no claim at all.

## 1.13.1 — 2026-10-19
- **Fixed: BitLocker volumes were all shown simply as "encrypted".** The BitLocker signature on the disk only
  says a volume was set up with BitLocker. DriveScope now asks Windows for the real state and shows it:
  **locked** (needs the password / recovery key), **on, unlocked on this PC**, or **protection OFF – readable by
  anyone** (suspended, or Windows 11 Device Encryption "waiting for activation": the key sits unprotected on
  the drive, so any PC can open it). For unlocked volumes DriveScope now also reads which Windows is installed
  and the user accounts, through Windows' own read-only file access.

## 1.13.0 — 2026-10-19
- **New: the drive's interface generation on the label** – in the big line next to the capacity, e.g.
  "1 TB SSD · NVMe PCIe Gen4 x4", "SATA III (6 Gb/s)", "USB flash drive · USB 3.2 Gen 1 (5 Gbps)".
  Read from the drive's own PCIe/SATA link when connected directly; for NVMe drives in a USB dock (which hides
  the PCIe link) it comes from the model number – including OEM part numbers such as Kingston OM8PGP4… (Gen4)
  – or, failing that, is estimated from the maker's rated speed. The screen shows how it was found.

## 1.12.3 — 2026-10-19
- **Fixed: the serial-number confirmation could never match on some drives.** Some drives and USB bridges
  (seen with a Kingston NVMe in a Realtek RTL9210 dock) pad the serial number with invisible characters, so the
  "last 4 characters" were invisible ones. Invisible characters are now removed from serials, models and
  firmware everywhere, and the confirmation code only counts letters and digits.

## 1.12.2 — 2026-10-19
- **Fixed: starting a new version kept showing the old one.** If DriveScope was already running (in the tray),
  starting a newer DriveScope.exe only opened the old copy's window – so updates and fixes never appeared.
  Now a different version or build closes the running copy and takes over (if the old copy is in the middle
  of a test or erase, it asks first). Starting the same version again still just opens its window.

## 1.12.1 — 2026-10-19
- **Fixed: "Prepare for sale" / "Remove all partitions" did nothing after typing the serial code.** Pressing
  Enter in the code box triggered the dialog's Cancel button, closing it silently. Enter now runs the
  operation when the code matches; the box shows "✔ matches" / "✖ doesn't match" as you type.
- **Fixed:** looking for an installed operating system (new in 1.11) shared the time limit of the drive's
  first read, so on a slow drive it could time out and the drive was wrongly marked "not responding",
  greying out the partition buttons. It now has its own time limit and can never block the drive.
- When the partition buttons are greyed out, a line now says why. When the identity check fails, the
  dialog has a "Rescan this drive and check again" button instead of only "close and refresh".
- Drives without a usable serial number now clearly ask you to type ERASE.

## 1.12.0 — 2026-10-18
- **New: "USB connection & controller" card** for flash drives, memory card readers and USB docks:
  - three speed bars: the speed it is **running at now**, the fastest **the drive supports**, and what **the
    USB port** it's plugged into supports – with plain advice when it runs slower than it could ("drive is
    USB 3 but connected at USB 2 speed – reinsert / avoid hubs", "this port is USB 2.0 only – about 10× faster
    in a USB 3 port", "the drive itself is USB 2.0").
  - **controller chip** (Phison, Silicon Motion, Alcor, Chipsbank, Innostor, ITE, Realtek…, by USB ID and
    firmware text), who sells the drive, the drive's own manufacturer / product / serial strings, USB version,
    controller revision, transfer mode (UAS / BOT), power requested, USB-A or USB-C port, hubs in between and
    the computer's USB controller.
  - **write protection**: drives that have locked themselves read-only (how flash drives usually die) are flagged.
  - **flash memory**: USB drives don't report their memory type; DriveScope says so and, after a benchmark,
    estimates the class of memory from the write speeds.
  All read-only – the same information Windows' USB tree holds (as Microsoft's USBView shows it).

## 1.11.0 — 2026-10-18
- **New: which operating system is installed on a drive.** DriveScope now looks inside the partitions and shows
  each system it finds:
  - **Windows** – the exact name (Windows 10 / 11 / Server…), edition, version and build (e.g. "23H2 · build
    22631.4317"), install / last-upgrade date, registered owner, computer name, last shutdown and the user accounts
    in C:\Users – read from the drive's own registry.
  - **Linux** – distribution and version (e.g. "Ubuntu 24.04.1 LTS"), computer name and the user folders in /home.
  - **Mac (APFS/HFS+), BitLocker and encrypted Linux** are named, with a note that their contents can't be read.
  - The **EFI boot partition's menu entries** (Windows Boot Manager, Ubuntu, Fedora…) are listed too.
  A warning appears when the drive still holds the previous owner's user accounts ("secure-erase before selling"),
  in the partition section and on the resale checklist. Everything is read straight from the raw sectors –
  DriveScope never mounts the drive or opens its files through Windows, so nothing on it changes.
- **New: "Not in Explorer" explanations.** Every partition without a drive letter now says why Windows Explorer
  doesn't show it (boot/reserved/recovery partition, "no drive letter" flag in the partition table, BitLocker,
  a Mac/Linux file system, or simply no letter assigned). The partition table's hidden / no-drive-letter /
  read-only flags are shown.

## 1.10.1 — 2026-10-18
- **Fixed:** "Could not list drives: Cannot read properties of null (reading 'length')" on some PCs. A drive with
  an empty list of something (no partitions, no S.M.A.R.T. attributes, no log entries…) was sent to the screen as
  "nothing" instead of "an empty list", and the screen stopped. The program now always sends empty lists, and
  the screen also tolerates them on its own.

## 1.10.0 — 2026-10-18
- **New: test several drives at once.** Every drive can run its own test, benchmark, burn-in, erase, refresh or
  partition change at the same time as the others. Each job has its own progress, Cancel button and
  "is the drive still answering" watchdog – a drive that hangs is still caught (and failed) while the others carry
  on. A second job on the same drive is refused. Busy drives show their task and progress in the drive list; the
  floating badge lists every running job (click one to jump to it); Windows notifies you as each one finishes, and
  each drive's before/after health snapshot is taken separately.
- **New: SATA Secure Erase** – the drive's own erase command (enhanced mode when supported), which also clears
  remapped sectors and spare areas and returns SSDs to factory speed. Works when the drive is not "frozen": drives
  plugged into a dock or hot-swap bay after Windows started usually qualify (DriveScope explains how to unfreeze one
  that was connected at boot). Uses a temporary password that the erase clears; if anything fails, the password is
  removed automatically, and a "Remove DriveScope password" button recovers a drive after an interruption.
  Verified before/after like the other erase methods, with a certificate.

## 1.9.0 — 2026-10-18
Reliability tools.
- **New: health before/after.** Key health counters are recorded when DriveScope first sees a drive (intake) and
  before/after every test, erase and partition change, kept per drive. If reallocated/pending/uncorrectable
  sectors, media errors or critical warnings go up while you test, the drive is marked **Do NOT resell** – even
  if every test passed. Resale rows "Health since intake" and "Health during last test"; "Health trend: Stable ✔"
  can appear on the label.
- **New: cable-error tracking.** S.M.A.R.T. #199 (CRC) is shown separately; a rise points at the cable or dock,
  not the drive.
- **New: the drive's own history** – error log (what went wrong and when, decoded) and self-test history, for
  NVMe (log pages 01h/06h) and SATA (SMART logs 01h/06h), direct and through docks. Harmless entries are greyed out.
- **New: burn-in (soak) test** – 1 to 12 hours of verified reading with hourly pattern writes and random I/O,
  temperature read every minute and graphed with the speed, slowdown-when-hot detection, health compared before and
  after. Wear stays negligible (≈16 GB written per hour).
- **New: data refresh** – reads every block and writes the same data back (data kept). Hard drives: deals with weak
  ("pending") sectors; optional zero-fill of unreadable blocks so the drive can replace them. SSDs: restores the
  speed of old, slow-to-read data.
- **New: hidden capacity (HPA/DCO)** check for SATA drives (direct and in docks), with a **Remove hidden area**
  button for drives connected directly by SATA (permanent, identity-verified, serial confirmation).
- **New: NVMe Sanitize** (block erase or crypto erase, incl. spare areas) in Secure erase, with the drive's own
  progress shown.
- **New: firmware help** – link to the maker's update tool for each brand; more known-bad firmware versions
  (Samsung 870 EVO SVT01B6Q, WD SN770 731030WD).
- **New: printable test report** – one page per drive (verdict, identity, health and trend, tests performed,
  benchmark, erase certificate, full resale checklist); print or save as PDF; kept in the "Test reports" folder.
- **New:** DriveScope's version number on the printed label (setting, on by default).

## 1.8.3 — 2026-10-18
- **Safety: nothing ever defaults to Windows Disk 0.** Every request that acts on a drive must name it explicitly –
  a missing, empty or malformed drive number is refused ("No drive was specified – nothing was done") instead of
  silently becoming 0. Requests for Disk 0 must also carry the fingerprint of Disk 0 exactly as the screen showed it,
  i.e. proof that you clicked it. The screen never selects Disk 0 by itself (not at start-up, after a refresh, or when
  drives are plugged in or removed); if no other drive is connected, nothing is selected.

## 1.8.2 — 2026-10-18
- **New: live progress inside each tool box.** The benchmark box shows an animated panel while it runs: moving
  progress bar, elapsed time, the test in progress with its live speed ("4,427 MB/s now · test 5 of 8 · 1 s left"),
  and the results table filling in as each test finishes. Previously each 5-second test sent no updates, so the
  screen looked frozen. The sustained write test and surface graph draw their graph live; self-test, erase and fake
  check also show their progress in their own boxes.
- **New: floating status badge** (bottom-right) whenever anything is running – what, which disk, percent and time –
  visible wherever you are on the page; click it to jump to the running test.

## 1.8.1 — 2026-10-18
- **New: partition dialog.** Format / Create / Prepare for sale / Delete / Remove all now open a dialog that shows
  the drive (verified on the hardware), exactly what will happen, a choice of format with plain-English pros and
  limits – exFAT (recommended for resale), NTFS, FAT32 (disabled above 32 GB) – a volume label, a GPT/MBR choice
  (GPT recommended) where it applies, and a box for the last 4 characters of the serial. The Go button stays off until
  the code matches. Previously the format came silently from drop-downs below the buttons.
- **New: live progress for partition changes** – an animated step list (verify → Windows double-check → remove →
  partition table → create → format → drive letter → re-read) with a moving progress bar and timer, and the disk is
  shown as "Working…" in the Disk Management view. Windows reports each step as it happens.

## 1.8.0 — 2026-10-18
- **New: system-tray app.** No more console window. DriveScope sits in the system tray (bottom-right of the
  taskbar): click the icon to open the page, right-click for Open / Copy address / Quit. Quit is also on the page.
  Closing the browser tab leaves it running in the tray.
- **New:** fixed address `http://127.0.0.1:47800/` (bookmarkable; falls back to a free port if taken). Starting
  DriveScope while it's already running just reopens the page instead of starting a second copy.
- **New:** a Windows notification when a long job finishes (read test, fake check, self-test, erase, benchmark,
  sustained write, surface graph, partition change), so you can work on something else meanwhile.
- Start-up errors are shown in a message box (there is no console to print them to).

## 1.7.1 — 2026-10-18
- **New: drive identity verification before every change.** Before any write (partition tools, secure erase, fake
  capacity checks, benchmarks/sustained writes on a blank drive) DriveScope re-reads the drive from the hardware and
  compares: exact size, the serial and model the device itself reports, the partition table's unique ID (tells two
  identical drives apart, even in docks without serial numbers) and that it doesn't hold Windows. Any mismatch
  stops the operation with nothing changed. The browser also sends the exact drive it displayed; if a rescan moved
  disk numbers, the request is refused. Partition operations additionally check Windows' unique disk ID and serial
  inside the Windows command itself.
- **New:** the partition section starts with a large identity bar – "Windows Disk N", model, size, serial,
  firmware, connection – and shows when the identity was last verified on the hardware. Every confirmation repeats
  the drive's identity, its current partitions and the verification result. Every box that can write shows its
  target drive.
- **New: Disk Management-style layout** – all disks stacked like Windows Disk Management (Disk N · Basic · size ·
  Online, navy partition bars, black unallocated, the same status wording and binary GB sizes), so it can be compared
  directly with Disk Management. Click a disk to select it. Plus Disk Management's volume list (Volume, Layout, Type,
  File System, Status, Capacity, Free Space, % Free) with Format / Delete / Create buttons.
- Partitions are matched to Windows volumes by exact position (not by size); damaged partition tables and
  non-responding drives are shown as such instead of as "unallocated".

## 1.7.0 — 2026-10-18
- **New: Partitions & file systems** – reads the partition table (GPT or MBR, including logical partitions) and
  identifies each file system by its signature, including ones Windows can't read: Mac APFS / HFS+, Linux ext2/3/4,
  XFS, Btrfs, swap, LVM, LUKS, plus NTFS, exFAT, FAT, ReFS and BitLocker. Shows labels and GPT names, a colour
  partition map, free space and which drive letter each partition has.
- **New: "Came from"** – works out what kind of computer the drive was used in (Windows system or data drive, Mac
  startup drive, Linux system, dual-boot, camera/console card, blank) with the reasons. The resale check flags Mac
  and Linux drives that need reformatting for Windows buyers; the label's Format/Platform lines use this too.
- **New: Partition tools** – delete or format a partition, create a partition in free space, remove all partitions,
  and "Prepare for sale" (remove everything → one exFAT/NTFS/FAT32 partition on GPT or MBR, with a label). Uses
  Windows' own storage engine; never available on the boot/system drive; every change needs the last 4 characters of
  the serial number; the drive's size is re-checked right before acting.
- **New: Standard and Features** (as in CrystalDiskInfo) – e.g. "NVM Express 1.4" or "ACS-3 | ACS-3 R5", and
  S.M.A.R.T., TRIM, VolatileWriteCache, NCQ, Self-test, Sanitize … with a plain-English explanation for each.
- **New: Complete drive information** panel – everything the drive reports, grouped: identity, connection, capacity
  and sector layout, cache and DRAM (NVMe drives that borrow host memory are shown as DRAM-less), maker's rated speed
  and flash type, temperature limits, power states, firmware slots, security/erase state (incl. ATA password lock),
  health and usage. Includes a drawing of the drive's form factor, a link to photos of the exact model, and
  "Copy all as text" for listings.

## 1.6.0 — 2026-10-18
- **New: Sustained write test** – writes one long stream (up to 16 / 64 / 256 GB, never more than half the drive)
  and graphs the speed. Finds the size of the drive's write cache and the speed after it, and names the drive class
  (good sustained speed / budget QLC or DRAM-less / very slow). Stops early once the slow part has been measured.
  Uses a temporary test file (existing data untouched) or writes directly to a blank drive after confirmation.
- **New: Surface read graph** – read-only speed graph across the whole drive (200 sampled areas, or every byte).
  Flags slow areas (hard drives are compared with their normal outer-to-inner slope) and read errors. Slow areas
  make the resale verdict "check first"; read errors make it "do not resell".
- **New: Speed score** – benchmark results are compared with the maker's rated speed (table of ~50 popular drive
  families, with flash type and DRAM) and with the connection's limit (SATA, PCIe link, USB dock chip), so a fast
  NVMe drive in a 10 Gbps dock is scored against the dock. Results faster than the connection allows are marked
  unreliable instead of scored.
- **New: Performance history** – every benchmark, sustained write and surface graph is saved per drive (by serial
  number) in `drivescope-performance-history.json` and shown under the tests.
- **New:** the label can show the speed score and sustained write speed (setting: "Show speed score & sustained
  write", applies instantly). Graphs have hover read-outs. The diagnostic file includes the new results and history.

## 1.5.2 — 2026-10-17
- **Fix:** the fake capacity check could call a genuine drive FAKE when Windows refused the test writes (for example
  because something still had the drive's volume open): each refused write was counted as "data didn't stick".
  Refused writes now give **Check not completed** with Windows' exact error message, never FAKE – except when the
  drive refuses only everything beyond a certain point, which is how some fakes behave.
- **Fix:** the quick fake check now restores original data from a properly aligned buffer, so the restore can't be
  rejected by Windows' direct-write mode.
- **Change:** the Refresh button now gives a clean slate – earlier read test, fake check, self-test, erase and
  benchmark results are cleared (a test still running is kept) and S.M.A.R.T. is read again for every drive.

## 1.5.1 — 2026-10-17
- **Change:** after every rescan (Refresh button or automatic plug/unplug detection) the boot/Windows drive is never
  left selected. A drive that just appeared is selected automatically; otherwise the non-boot drive you were
  looking at stays selected; otherwise the first non-boot drive is chosen.

## 1.5.0 — 2026-10-17
- **New:** hover any S.M.A.R.T. value to see the raw number exactly as CrystalDiskInfo shows it (12 hex digits)
  plus its decimal value. NVMe fields now show CrystalDiskInfo's ID (01–11) before the name, and ATA IDs are shown
  in CrystalDiskInfo's hex form, so the two programs can be compared line by line.

## 1.4.3 — 2026-10-17
- **Fix:** Realtek RTL9210 docks (e.g. Sabrent) also invent a SATA-style ID for NVMe drives, with stray numbers that
  got past the 1.4.2 check. Detection is now stricter (a real SATA ID always reports LBA support and its features),
  and whenever SATA-style health data fails on a dock chip that can hold NVMe drives, the NVMe commands are tried
  before giving up. Checked against CrystalDiskInfo's readings of the same drive (Toshiba KXG50 in a Sabrent dock).

## 1.4.2 — 2026-10-17
- **Fix:** Realtek RTL9220 docks invent a SATA-style ID (name, serial and firmware only) for NVMe drives. DriveScope
  took it as a SATA drive and never asked for the NVMe health data. It now recognises the invented ID and goes on to
  the Realtek NVMe commands; if those are blocked too, it says so plainly. The diagnostic file records every attempt.

## 1.4.1 — 2026-10-17
- **Fix:** 1.4.0 would not start ("side-by-side configuration is incorrect"). The version number had been written
  into the manifest's XML header instead of the program's identity line. The build now validates the manifest and
  an automated test checks the template, so this can't ship again.

## 1.4.0 — 2026-10-17
Several updates on 17 Oct were mistakenly all labelled 1.3.0; this release gathers them under a new number.
- **Fix:** power-on hours, temperature and life remaining now come from the drive's own S.M.A.R.T. data first.
  Windows' reliability counters (which often report 0 for "not supported") are only a fallback, and a lone
  Windows 0 is treated as unknown – no more "0 hours" or false "100% life left".
- **New:** impossible S.M.A.R.T. data (e.g. −273 °C, 0% spare with no alarm, wear with zero use) is rejected and
  shown as **NOT VALID** instead of being judged; it is never used for the verdict, hours, temperature or life.
- **Fix:** an NVMe drive whose spare is below its threshold is now FAILED overall (was PASSED with a failing row).
- **New:** JMicron JMS583 docks – the health log is retried in alternative standard forms; dock rating warns that
  JMS583 health data can be unreliable; the connection card says "S.M.A.R.T. returned, but not valid".
- **New:** "Save diagnostic file" – exports everything about a drive, including the raw bytes the drive/dock returned.
- **New:** plain-English explanations under the Interface and Form factor lines.
- **New:** single-source versioning (`VERSION` + `build.sh`), build stamp in the footer, console and exe properties.

## 1.3.0 — 2026-10-17
- Drive's built-in self-test (short / extended) for SATA, SATA-in-dock and NVMe.
- Secure erase: overwrite + verify + TRIM (NIST Clear) or NVMe cryptographic erase (NIST Purge), with a printable
  erase certificate.
- CrystalDiskMark-style benchmark (SEQ1M Q8T1, SEQ1M Q1T1, RND4K Q32T1, RND4K Q1T1; read and write) with an
  expected-speed check.
- Total data written (TBW) for SATA drives; counterfeit SSD check (brand vs controller / hardware ID / capacity).
- Full code documentation and README.
- Plain-English explanation for every S.M.A.R.T. value.

## 1.2.0 — 2026-10-17
- Tests all drive types: SSDs, hard drives, USB flash drives and memory cards.
- Fake capacity detection: risk hints, read-only wraparound check, quick fake check (restores data), full verify.
- Direct printing to Brother QL-800/810W/820NWB on 62 mm tape (USB via Windows or Wi-Fi).

## 1.1.0 — 2026-10-17
- Renamed to DriveScope; icon, Dialsoft LLC metadata, administrator manifest.
- USB dock pass-through (SAT for SATA; ASMedia/JMicron/Realtek for NVMe) and dock quality rating.
- Connection & S.M.A.R.T. access card; all S.M.A.R.T. values in Drive details; boot-drive protection;
  automatic refresh on drive/dock changes; resale check; firmware status; activity animations.

## 1.0 — 2026-10-17
- First version (as "SSD Tester"): drive list, read test, S.M.A.R.T. summary, 4 × 2.4 in label.
