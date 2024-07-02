# ConvertFrames2OneHotFormat
I extract frames from a video using FFmpeg and identify interesting behaviors frame-by-frame. I then use the Jupyter script provided here to parse out the frame numbers and create an annotation CSV, which can be imported into our A-SOID project.

The script is divided into two main parts:

Sequence Extraction from Image Files: This part of the script extracts sequences of consecutive images from a directory. The script assumes that the images are named in a specific format, where the name ends with a number followed by the “.png” extension. The script extracts these numbers, identifies sequences of consecutive numbers, and writes these sequences to a CSV file.
Behavior Binary Array Creation: This part of the script reads the CSV file created in the first part and creates binary arrays for each unique behavior in the data. The binary arrays represent the presence or absence of a behavior at each time step in the video. The time steps are in units of 0.1 seconds. The binary arrays are then saved as separate CSV files.
Here’s a more detailed breakdown:

# Part 1: Sequence Extraction from Image Files

The script first specifies the directory where the image files are located.
It then gets a list of all filenames in the directory and filters out files that aren’t .png.
The filenames are sorted in ascending order.
A regular expression matches the number at the end of each filename.
The script then iterates over the filenames. For each filename, it extracts the number at the end of the filename. If this is the first file or if the number is not consecutive with the previous number, it starts a new sequence. Otherwise, it continues the current sequence.
Finally, it writes the sequences to a CSV file. Each row in the file represents a sequence and contains its start number, stop number, and length.

# Part 2: Behavior Binary Array Creation

The script loads the CSV file created in the first part.
It checks if the maximum frame number in the data exceeds the total number of frames in the video.
It calculates the total duration of the video in time steps of 0.1 seconds.
It creates a binary array for each unique behavior in the data, which is initially filled with zeros.
It then iterates over the data rows. For each row, it converts the start and stop frame numbers to time steps of 0.1 seconds and fills in the corresponding section of the binary array with ones.
Finally, it saves each binary array as a separate CSV file, each containing a time column and a behavior column.
