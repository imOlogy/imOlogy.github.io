
# SOS Game Tracking System

A real-time Computer Vision application that acts as an automated referee for the physical pen-and-paper game "SOS". This system analyzes a live video feed to track the game board, detect moves ('S' or 'O'), and determine the winner automatically. The project is developed as part of the Digital Image Processing course offered by Prof. Dr. İbrahim Delibaşoğlu at the Software Engineering department at Sakarya University in the Fall of 2025-2026.


## Key Features

* **Real-Time Computer Vision**: Utilizes OpenCV to process live video feeds, applying perspective transformation to generate a "bird's-eye view" of the game board.
* **Intelligent Grid Analysis**: Automatically detects the grid lines and coordinates to map physical board cells to digital game logic.
* **Optical Character Recognition (OCR)**: Integrates both **Tesseract** and **SVM (Support Vector Machine)** models to recognize handwritten 'S' and 'O' characters.
* **Automated Game Logic**: Maintains the state of the game, validating moves and checking for winning "SOS" sequences (horizontal, vertical, or diagonal) in real-time.
* **Robust Logging**:
* **Visual Logs**: Saves images of every move with HUD overlays showing the score.
* **Data Logs**: Exports a detailed `.txt` log of the entire session, including board states and move history.


## System Requirements

* **OS**: Windows 11 (Recommended)
* **Language**: C++17
* **Build System**: CMake (3.10+)
* **Libraries**:
* OpenCV (4.x)
* Tesseract 5.5 & Leptonica 1.86


## Project Structure

* **`src/`** & **`include/`**: Core source code for the game pipeline, image processing, and logic.
* **`training_workspace/`**: A separate toolkit for collecting training data and training the SVM model (`DataCollector`, `TrainSVM`).
* **`bin/`**: Contains the compiled executable and the `sos_model.xml` (SVM model).
* **`logs/`**: Stores session logs and screenshots of game moves.
* **`build.bat`**: Automated script for initializing, building, and running the project.


## Configuration

Before building, ensure your environment is set up correctly.

1. **OpenCV**: Ensure you have a valid OpenCV build.
* Set the `OPENCV_BUILD_DIR` environment variable, or define it in a `.env` file in the root directory.


2. **Tesseract**: The project currently points to a specific Tesseract SDK path.
* Open `CMakeLists.txt` and update the `TESS_SDK` variable to point to your local Tesseract installation:
```cmake
set(TESS_SDK "C:/Path/To/Your/Tesseract/SDK")
```

* *Note: Ensure the library names in `target_link_libraries` match your specific version (e.g., `tesseract55`, `leptonica-1.86.0`).*

  
**Model Selection (Switching OCR)**

The system supports two different engines for recognizing 'S' and 'O' characters. You can switch between them by modifying the source code configuration:

1. Open the configuration file: `include/Config.hpp`.
2. Locate the `ACTIVE_OCR_MODE` constant at the bottom of the file.
3. Change the value to your desired mode:
```cpp
// Option A: Use Tesseract (Best for general compatibility)
const OCRMode ACTIVE_OCR_MODE = MODE_TESSERACT;

// Option B: Use Custom SVM (Requires sos_model.xml)
const OCRMode ACTIVE_OCR_MODE = MODE_SVM;
```


## Build & Run Instructions

This project includes a convenience script (`build.bat`) to handle the CMake workflow directly from the Windows Command Prompt (cmd).

### 1. Initialize the Project

Open `cmd` in the project root and run the initialization step. This creates the visual studio solution files.

```cmd
build.bat init
```

### 2. Build the Application

Compile the source code in Release mode. This step also attempts to automatically copy the necessary OpenCV DLLs to the binary folder.

```cmd
build.bat build
```

### 3. Run the Game

Execute the main program. This will open the camera feed and start the game pipeline.

```cmd
build.bat run
```

*Note: The script automatically handles directory navigation to ensure the application finds necessary assets like `sos_model.xml`.*


## Controls & Usage

1. **Setup**: Place the SOS game grid on a flat surface visible to the camera.
2. **Gameplay**: Players take turns writing 'S' or 'O' in empty cells.
3. **Visual Feedback**:
* The system highlights the detected grid.
* New moves are boxed and labeled.
* Winning "SOS" lines are drawn on the screen.
4. **Termination**: The game ends when the board is full or the application is closed. Check the `logs/` folder for a record of the match.


## Training Custom Models (Optional)

If you wish to improve detection accuracy by training your own SVM model, navigate to the `training_workspace` folder.

1. **DataCollector**: Run this to capture cropped images of 'S', 'O', and empty cells from your specific camera setup.
2. **TrainSVM**: Run this to generate a new `sos_model.xml` based on your collected data.
3. **Deployment**: Copy the generated XML file to the `bin/` directory of the main project.

---


## Author Info

**Name:** Mahfuz AHMAD
**Student ID:** B221210591
**Department:** Computer Engineering
**University:** Sakarya University
**Course:** Digital Image Processing (Fall 2025-2026)
