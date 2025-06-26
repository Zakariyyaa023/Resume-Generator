# Pollinations.AI Code Generator Webpage

This project is a web application that leverages [Pollinations.AI](https://pollinations.ai) to generate code from a user's prompt. It provides an interactive split-screen interface where:

- The **left side** shows the generated code based on the user's input.
- The **right side** displays a live preview of the running code output.

Additionally, users can export the generated code and output as a Word `.docx` document for further editing and use.

---

## Features

- 📝 **Prompt-based code generation** using Pollinations.AI.
- 🖥️ **Split-screen layout**:  
  - Left: Editable generated code  
  - Right: Live rendered output of the code
- 💾 **Export to Word (.docx)**: Save your work and edit it later in Word or compatible editors.

---

## How It Works

1. User enters a descriptive prompt about the code they want.
2. The app sends the prompt to Pollinations.AI and receives generated code.
3. The code appears on the left panel, where it can be edited if needed.
4. The right panel renders the code live so users can see the output immediately.
5. Users can click a button to export the current code and output into a Word document (`.docx`).

---

## Usage

1. Clone or download this repository.
2. Open `index.html` in your favorite browser.
3. Enter a prompt describing the code you want.
4. Generate and view the code and its output.
5. Click **Save as Word** to download the project as a `.docx` file.

---

## Example Prompts

- "Create a simple HTML page with a header and a button."
- "Write JavaScript to create a countdown timer."
- "Design a CSS animation for a bouncing ball."

---

## Technologies Used

- HTML, CSS, JavaScript
- Pollinations.AI API
- Word export functionality (using Blob and custom HTML wrappers)
- iframe sandbox for live preview

---

Made with 💡 and Pollinations.AI
