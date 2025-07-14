
// This will be using to get information on the html to function on
const promptBtn = document.querySelector(".prompt-btn");
const promptInput = document.querySelector(".prompt-input");
const textArea = document.getElementById("generatedText");
const generateBtn = document.querySelector(".generate-btn");
const downloadBtn = document.getElementById("savePdfBtn");
const showLiveCode = document.getElementById("codePreview");

// Examples that the user can use to generate resumes
const examplePrompts = [
  "Create a professional resume for a senior software engineer with 10 years of experience in backend development using Java and Python.",
  "Generate a modern resume for a recent marketing graduate with internship experience and strong digital media skills.",
  "Write a tailored resume for a data analyst applying to a tech company, highlighting skills in SQL, Python, and Tableau.",
  "Build a resume for an experienced HR manager with a focus on talent acquisition, training, and employee engagement.",
  "Create a resume for a nurse with 5+ years of experience in emergency care and certifications in ACLS and BLS.",
  "Generate a resume for a remote customer service representative with strong communication skills and CRM experience.",
  "Write a compelling resume for a high school teacher transitioning into instructional design.",
  "Build a resume for a cybersecurity specialist with experience in penetration testing, risk assessment, and compliance frameworks.",
  "Create a resume for a financial analyst with strong Excel and Power BI skills applying to an investment firm.",
  "Generate a creative resume for a UX/UI designer with a background in Figma, Adobe XD, and user research.",
  "Write a resume for a project manager with PMP certification, 8 years of experience, and expertise in Agile and Scrum.",
  "Build a resume for a mechanical engineer seeking opportunities in renewable energy projects.",
  "Create a professional resume for a lawyer with a focus on intellectual property and contract law.",
  "Generate a resume for a sales executive applying for a SaaS company, with emphasis on quota achievements and lead generation.",
  "Write a resume for a business analyst with strong stakeholder management and experience in agile environments.",
  "Build a resume for a junior web developer with experience in HTML, CSS, JavaScript, and React.",
  "Create a resume for an executive assistant with 15 years of experience supporting C-level executives.",
  "Generate a resume for a content writer with SEO experience and published articles in tech and business blogs.",
  "Write a resume for an environmental scientist applying to a sustainability consulting firm.",
  "Build a resume for a logistics coordinator with expertise in inventory management, vendor relations, and supply chain optimization."
];

// This will randomly select one example prompt and animate it into the prompt box using 10 speed.
promptBtn.addEventListener("click", () => {
  const prompt = examplePrompts[Math.floor(Math.random() * examplePrompts.length)];
  let i = 0;
  promptInput.focus();
  promptInput.value = "";
  promptBtn.disabled = true;
  promptBtn.style.opacity = "0.5";
  const typeInterval = setInterval(() => {
    if (i < prompt.length) {
      promptInput.value += prompt.charAt(i);
      i++;
    } else {
      clearInterval(typeInterval);
      promptBtn.disabled = false;
      promptBtn.style.opacity = "0.8";
    }
  }, 10);
});

// this will auto scroll down when being typed into the Text area
promptInput.addEventListener('input', () => {
  promptInput.style.height = 'auto';
  promptInput.style.height = promptInput.scrollHeight + 'px';
});

//connects to pollinatios.ai and then get the response ,encodes it to send disables a btn so it won't spam send to the api
const generateTextCode = async (promptText) => {
  generateBtn.disabled = true;
  let i = 0;
  let generatedText = "";

  try {
    const encodedPrompt = encodeURIComponent(promptText);
    const baseURL = `https://text.pollinations.ai/prompt/${encodedPrompt}`;
    const response = await fetch(baseURL, {
      method: "GET",
      headers: {
        "Accept": "text/plain",
      },
    });

    if (!response.ok) {
      throw new Error("Text generation failed");
    }

    generatedText = await response.text();

    // ✅ Strip Markdown fences ```html ... ```
    const cleanText = generatedText
      .replace(/^```html\s*/i, '') // remove ```html
      .replace(/```$/, '')         // remove trailing ```

    const textArea = document.getElementById("generatedText");
    if (textArea) {
      textArea.value = "";
      const trimmed = cleanText.trim().toLowerCase();
          if (trimmed.startsWith("<") || trimmed.startsWith("<!doctype") || trimmed.startsWith("<style")) {
            renderCodeInIframe(cleanText);
          } else {
            console.warn("Pollinations response is not valid HTML/CSS code.");
            textArea.value += "Preview skipped: The response doesn't appear to be valid code.";
          }
      // Typing animation
      const typeInterval = setInterval(() => {
        if (i < cleanText.length) {
          textArea.value += cleanText.charAt(i);
          textArea.scrollTop = textArea.scrollHeight;
          textArea.style.height = textArea.scrollHeight + "px";
          i++;
        } else {
          clearInterval(typeInterval);
          generateBtn.disabled = false;

          // ✅ Check after cleaning, not original!
          
        }
      }, 5);
    }
  } catch (error) {
    console.error("Error generating text/code:", error);
    const textArea = document.getElementById("generatedText");
    if (textArea) {
      textArea.value = "// Error generating code. See console.";
    }
    generateBtn.disabled = false;
  }
};

// this then dispay code into a iframe on the right showing a preview of what the user can save
function renderCodeInIframe(codeString) {
  const iframe = document.getElementById('codePreview');
  const doc = iframe.contentDocument || iframe.contentWindow.document;

  // Remove Markdown fences if any
  const withoutFences = codeString
    .replace(/^```html\s*/i, '')
    .replace(/```$/, '');
  const scriptRegex = /<script\b[^>]*>[\s\S]*?<\/script>/gi;
  const codeWithoutScripts = withoutFences.replace(scriptRegex, '');

  // Remove inline event handlers like onclick
  const sanitized = codeWithoutScripts
    .replace(/\son\w+="[^"]*"/gi, '')
    .replace(/\son\w+='[^']*'/gi, '');

  doc.open();
  doc.write(sanitized);
  doc.close();
  iframe.style.height = "auto";
  setTimeout(() => {
    const body = doc.body;
    if (body) {
      iframe.style.height = body.scrollHeight + "px";
    }
  }, 50);
  
}
//downloads the file so the user can edit it
document.getElementById('savePdfBtn').addEventListener('click', () => {
  const iframe = document.getElementById('codePreview');
  const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
  const htmlContent = iframeDoc.documentElement.outerHTML;

  const header = `
    <html xmlns:o='urn:schemas-microsoft-com:office:office' 
          xmlns:w='urn:schemas-microsoft-com:office:word' 
          xmlns='http://www.w3.org/TR/REC-html40'>
    <head><meta charset='utf-8'><title>Export HTML to Word</title></head><body>`;
  const footer = "</body></html>";

  const sourceHTML = header + htmlContent + footer;
  const blob = new Blob(['\ufeff', sourceHTML], {
    type: 'application/msword'
  });

  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url;
  link.download = 'Generated Resume.doc';
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
  URL.revokeObjectURL(url);
});

//handles the form submit making sure everything runs in order
const handleFormSubmit = async () => {
  const promptText = promptInput.value?.trim() || "";
  generateBtn.disabled = true;

  // Count only alphabetic letters (no spaces, numbers, symbols)
  const letterCount = (promptText.match(/[a-zA-Z]/g) || []).length;

  if (letterCount < 50) {
    alert("Please enter at least 50 letters (excluding symbols and spaces).");
    generateBtn.disabled = false;
    return;
  }

  const isValid = await isValidResumePrompt(promptText);
  if (isValid) {
    await delay(2000);

    // Strict instruction: only return HTML + CSS, with optional inline comments
    const cleanPrompt = `Only generate HTML and CSS code for this: ${promptText}. Do not include any explanation or extra text. Only output code (with optional inline comments). No JavaScript. End politely in comments only.`;

    await generateTextCode(cleanPrompt);
    textArea.classList.add("show");
    downloadBtn.classList.add("show");
    showLiveCode.classList.add("show");
  } else {
    alert("Please describe building a resume or describe how you want it to look.");
  }

  generateBtn.disabled = false;
};


//checks if the prompt is resume related and if so will continue if not it will aleart the broswer
async function isValidResumePrompt(prompt) {
  const question = `Only answer with yes or no, is this a Resume-related prompt or describing a resume? (${prompt})`;

  const encodedPrompt = encodeURIComponent(question);
  const url = `https://text.pollinations.ai/prompt/${encodedPrompt}`;

  try {
    const response = await fetch(url, {
      method: "GET",
      headers: { "Accept": "text/plain" }
    });

    if (!response.ok) throw new Error("Text generation failed");

    const text = (await response.text()).toLowerCase().trim();
    return text.includes("yes"); // More flexible
  } catch (error) {
    console.error("Error validating prompt:", error);
    return false;
  }
}


if (promptInput) {
  promptInput.addEventListener("submit", (e) => handleFormSubmit(e));
}

generateBtn.addEventListener("click", () => {
  handleFormSubmit()
});

const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
