# 🖥️ PSS Memory Usage Monitor

## 📝 Description
A bash script that provides detailed memory usage statistics for running processes on Linux systems, displaying results in a user-friendly format with progress bars and memory units (KB, MB, GB).

## 🎯 PSS vs Other Memory Metrics: A Quick Guide
PSS (Proportional Set Size) offers a more accurate view of memory usage compared to traditional metrics like RSS (Resident Set Size) and VSZ (Virtual Size). 📊

The key advantage of PSS is its fair handling of shared memory. While RSS double-counts shared pages and VSZ includes unused memory, PSS divides shared memory proportionally among processes using it. 🔄

Example:

For a 30MB shared library used by 3 processes:
- RSS: Shows 30MB for each process (90MB total)
- PSS: Shows 10MB per process (30MB total, accurate!)
- 
This makes PSS ideal for:

🎯 Accurate system memory monitoring
🐳 Container resource management
🔍 Memory leak detection
📊 Application profiling
The total PSS across all processes equals actual physical memory usage, making it the most reliable metric for real-world memory management. 💡

## 🎯 Features
- 📊 Displays PSS (Proportional Set Size) memory usage for processes
- 📈 Shows memory usage as percentage of total system memory
- 🎨 Visual progress bars for memory consumption
- 🔄 Automatic unit conversion (Ki, Mi, Gi)
- 🎯 Custom process grouping for better overview
- 📦 Aggregates small memory consumers into "others" category

## 🔧 Prerequisites
- Linux operating system
- `smem` utility installed
- `bc` calculator
- `sudo` privileges

## 📦 Installation
```bash
git clone https://github.com/LLSouf/pss/
cd pss
chmod +x ./pss
```
## 🚀 Usage
Run the script
```bash
./pss
```
## 📋 Output Format
```bash
rocess_name : memory_usage unit percentage% [progress_bar]
--------------------------------
TOTAL : total_memory_usage unit percentage% [total_progress_bar]
```
## ⚙️ Configuration
Custom process groups can be modified in the script by editing the appcust array:
```bash
appcust=("chrome" "discord" "python" "i3" "gvfs" "systemd" "at-spi" "vim")
```
## 📁 Cache Directory
The script creates and uses a cache directory at: ~/.cache/pss_usage/

## 🔍 Technical Details
Uses smem for accurate PSS memory information
Processes with memory usage < 1024KB are grouped under "others"
Progress bars scale according to total system memory (14.8GB default)
Supports dynamic unit conversion based on memory size

## 🛠️ Customization
Modify 15518924 value to match your system's total memory in KB
Adjust progress bar width by changing the multiplier in bartotval calculation
Edit the appcust array to track different processes

## 🐛 Known Issues
Requires sudo password for smem execution
Cache files need to be cleaned manually if script fails
