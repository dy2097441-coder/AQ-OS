AQ OS v1.2 🚀A custom, 16-bit bootable Operating System built in x86 Assembly. AQ OS was created strictly for fun and as a learning journey into low-level systems programming.✨ FeaturesCustom Welcome Text: A retro-style greeting on boot.Command Line Interface: A functional shell with several built-in commands.Time Display: Pulls real-time data from the BIOS system clock.Memory Storage: A save and read system that stores text directly in RAM.Safety Commands: Includes help, cls (clear screen), and shutdown.Readme Command: A special command inside the OS explaining its purpose.🛠 System RequirementsFor Development (Building the ISO):Operating System: Linux or Windows Subsystem for Linux (WSL).Assembler: NASM (Netwide Assembler).ISO Tools: xorriso or genisoimage.Compiler Tools: dd (standard on Linux/WSL).For Running the OS:Emulator: QEMU (Recommended), VirtualBox, or VMware.Hardware: Any x86-compatible machine (via USB/CD boot).🚀 How to Build and Run1. Install Dependencies (WSL/Ubuntu)Bashsudo apt update
sudo apt install nasm xorriso qemu-system-x86 -y
2. Compile the SourceBashnasm -f bin aq_os.asm -o aq_os.bin
3. Create the Bootable ISOBash# Create a folder for the ISO structure
mkdir -p iso_root

# Create a virtual 1.44MB floppy and inject the binary
dd if=/dev/zero of=iso_root/floppy.img bs=1024 count=1440
dd if=aq_os.bin of=iso_root/floppy.img conv=notrunc

# Generate the ISO file
xorriso -as mkisofs -R -b floppy.img -no-emul-boot -boot-load-size 4 -o aq_os.iso iso_root/
4. Run the OSYou can run the ISO directly from your terminal:Bashqemu-system-x86_64 -cdrom aq_os.iso
💻 Available CommandsCommandDescriptionhelpLists all available commands.readmeShows information about the OS creator.timeDisplays the current system time.savePrompts for text to save into RAM.readDisplays the last saved text.shutdownSafely turns off the machine (APM).📄 LicenseThis project is open-source and available under the MIT License. Feel free to fork it, break it, and learn from it!Note: This OS runs in "Real Mode." Saving data is volatile, meaning it will be erased once the system is rebooted or powered off.
