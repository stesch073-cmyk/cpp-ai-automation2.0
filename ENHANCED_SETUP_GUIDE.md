# Enhanced Unreal AI Architect - Setup & Usage Guide

## 🚀 What's New

Your original Unreal AI Architect has been enhanced with the C++ AI Automation Platform features:

### New Features Added

1. **ARCHITECT PRO** - Advanced C++ code generation with:
   - AI-powered validation
   - Quality scoring (0-100%)
   - Automatic .Build.cs generation
   - Engine compatibility checks
   - Iterative refinement support

2. **ERROR DOCTOR** - AI error handling:
   - Analyze compilation/linking errors
   - Auto-fix with multiple strategies
   - Root cause identification
   - Confidence scoring
   - Prevention tips

3. **BUILD MASTER** - Build system generation:
   - Automatic .Build.cs creation
   - Module dependency management
   - Step-by-step integration instructions

4. **4 Operating Modes**:
   - **Generate**: Create new C++ code
   - **Debug Error**: Analyze and fix errors
   - **Refine**: Improve existing code (up to 5 iterations)
   - **Build Files**: Generate build system files

5. **Enhanced UI**:
   - Session statistics tracking
   - API connection status
   - Code viewer with syntax
   - Validation report viewer
   - Mode selector

## 📋 Prerequisites

1. **Python 3.9+**
2. **C++ AI Platform Backend** (must be running)
3. **Unreal Engine** (optional, for full integration)

## 🔧 Setup

### Step 1: Install Python Dependencies

```bash
pip install -r requirements_enhanced.txt
```

### Step 2: Configure Environment

Create a `.env` file in the same directory:

```env
# Unreal Engine Connection (optional)
UNREAL_HOST=127.0.0.1
UNREAL_PORT=30010

# C++ AI Platform API (REQUIRED)
CPP_AI_API_URL=http://localhost:8000/api

# API Keys (REQUIRED for full functionality)
OPENAI_API_KEY=sk-your-openai-key-here
HUGGINGFACE_API_KEY=hf_your-huggingface-key-here
```

### Step 3: Start the C++ AI Platform Backend

**Option A: Using Docker (Recommended)**
```bash
# In the cpp-ai-automation directory
cd cpp-ai-automation
docker-compose up -d
```

**Option B: Manual Start**
```bash
cd cpp-ai-automation/backend
source venv/bin/activate
python app.py
```

Verify backend is running: http://localhost:8000/health

### Step 4: Run the Enhanced App

```bash
python unreal_ai_architect_enhanced.py
```

## 🎯 How to Use

### Mode 1: Generate Code

1. Select **"Generate"** mode
2. Enter your prompt:
   ```
   "Create an Actor that spawns particles on player overlap with 
   Blueprint-configurable particle system selection"
   ```
3. Click **EXECUTE**
4. Wait for generation (5-10 seconds)
5. Review code in **"Generated Code"** tab
6. Check validation in **"Validation"** tab
7. Code automatically saved to `assets/code_generated/`

**What You Get:**
- Generated C++ code (.cpp and .h files)
- Quality score (aim for 85%+)
- Validation report (issues, warnings, suggestions)
- Build files (.Build.cs)
- Instructions for Unreal integration

### Mode 2: Debug Error

1. Copy a compiler error from Unreal/Visual Studio:
   ```
   error C2027: use of undefined type 'UWorld'
   ```
2. Select **"Debug Error"** mode
3. Paste the error message
4. Click **EXECUTE**
5. Review analysis in **"Validation"** tab

**What You Get:**
- Error severity and category
- Root cause explanation
- 3 suggested fixes (ranked by confidence)
- Auto-fix attempt (if confidence > 70%)
- Fixed code saved to `assets/code_generated/Fixed_*.cpp`

### Mode 3: Refine Code

After generating code, improve it iteratively:

1. Generate code first (Mode 1)
2. Select **"Refine"** mode
3. Enter refinement instructions:
   ```
   "Add null pointer checks and optimize for performance"
   ```
4. Click **EXECUTE**
5. Repeat up to 5 times

**What You Get:**
- Improved code version
- List of improvements made
- Updated quality score
- Iteration tracking

### Mode 4: Build Files

Generate Unreal build system files:

1. Generate code first (Mode 1)
2. Select **"Build Files"** mode
3. Optionally specify module name
4. Click **EXECUTE**

**What You Get:**
- `ModuleName.Build.cs` file
- Module dependency list
- Step-by-step integration instructions
- Files saved to `assets/build_files/`

## 📊 Understanding the UI

### Connection Status

**🟢 UNREAL ONLINE** - Connected to Unreal Engine
**🔴 UNREAL OFFLINE** - Unreal not running (code generation still works)

**🟢 C++ AI API ONLINE** - Backend connected
**🔴 C++ AI API OFFLINE** - Backend not running (app won't work)

### Session Stats

- **Generated**: Total code generations this session
- **Errors Fixed**: Successful auto-fixes
- **Iteration**: Current refinement iteration count

### Tabs

- **Viewport**: Visual preview (for 3D assets)
- **Generated Code**: View generated C++ code
- **Validation**: Quality reports, error analysis, build instructions

## 🔄 Complete Workflow Example

### Scenario: Create a Custom Unreal Actor

**Step 1: Generate Initial Code**
```
Mode: Generate
Prompt: "Create an Actor with a static mesh component that can be 
configured in Blueprint. Add BeginPlay and Tick functions."
```
**Result**: Code generated, Quality: 78%

**Step 2: Check Validation**
- Switch to **Validation** tab
- Review warnings: "Consider adding null checks"
- Note: Requires review before production

**Step 3: Refine Code**
```
Mode: Refine
Prompt: "Add null pointer checks for the mesh component and 
optimize Tick function to only run when needed"
```
**Result**: Quality improved to 92%, Iteration 1

**Step 4: Generate Build Files**
```
Mode: Build Files
Prompt: "Create build files for this actor"
```
**Result**: `MyActor.Build.cs` generated with dependencies

**Step 5: Test in Unreal**
- Copy code from `assets/code_generated/`
- Copy .Build.cs from `assets/build_files/`
- Follow integration instructions
- Compile in Visual Studio

**Step 6: If Errors Occur**
```
Mode: Debug Error
Paste: [Your compiler error]
```
**Result**: Error analyzed, auto-fix applied, or fix suggestions provided

## 🎨 Advanced Features

### Batch Operations

Generate multiple related files:
```
1. Generate base Actor
2. Generate derived class (Refine with "Create a derived class")
3. Generate component (New generation)
4. Generate build files for each
```

### Error Learning

The system learns from your feedback:
- If auto-fix works → System improves
- If auto-fix fails → Try different strategy
- Patterns saved for future reference

### Quality Guidelines

**Quality Score Interpretation:**
- **90-100%**: Excellent - Minor review needed
- **80-89%**: Good - Standard review
- **70-79%**: Fair - Careful review required
- **<70%**: Poor - Consider regenerating

## 🐛 Troubleshooting

### "C++ AI API OFFLINE"

**Problem**: Red status for C++ AI API

**Solution**:
```bash
# Check backend is running
curl http://localhost:8000/health

# If not running, start it:
cd cpp-ai-automation
docker-compose up -d

# Or manually:
cd backend
python app.py
```

### "No code to refine"

**Problem**: Trying to refine without generating first

**Solution**: Generate code first using "Generate" mode

### "Generation takes too long"

**Problem**: Waiting 30+ seconds

**Causes**:
- API server slow/not responding
- Large code generation (increase timeout)
- Network issues

**Solution**:
- Check backend logs: `docker-compose logs backend`
- Verify OpenAI API key is valid
- Try simpler prompt

### "Code quality is low"

**Problem**: Getting quality scores < 70%

**Solution**:
1. Be more specific in prompt
2. Use refinement mode to improve
3. Check validation tab for specific issues
4. Try different AI model (if supported)

## 📁 File Structure

```
your_project/
├── unreal_ai_architect_enhanced.py  ← Main application
├── requirements_enhanced.txt         ← Python dependencies
├── .env                             ← Configuration
│
├── assets/
│   ├── code_generated/              ← Generated C++ files
│   ├── build_files/                 ← .Build.cs files
│   ├── models/                      ← 3D assets (original)
│   ├── audio/                       ← Audio files (original)
│   └── scripts/                     ← Other scripts
│
└── logs/                            ← Session logs
```

## 🔐 Security Notes

1. **Never commit .env file** - Contains API keys
2. **Review all generated code** - Don't use blindly in production
3. **Test in development** - Always test before deploying
4. **Backup your work** - Save important generations

## 🎓 Tips for Best Results

### Writing Good Prompts

**❌ Bad Prompt:**
```
"Make an actor"
```

**✅ Good Prompt:**
```
"Create a C++ Actor class for Unreal Engine 5.3 that:
- Has a UStaticMeshComponent
- Spawns particles on BeginPlay
- Includes UPROPERTY for Blueprint configuration
- Has proper null checks and error handling"
```

### When to Use Each Mode

**Generate**: Starting fresh, new features
**Debug**: Compiler errors, runtime crashes
**Refine**: Improving existing code, optimizations
**Build Files**: Setting up new modules, fixing dependencies

### Iteration Strategy

```
Generate (Quality 75%)
  ↓
Refine: "Add error handling" (Quality 82%)
  ↓
Refine: "Optimize performance" (Quality 88%)
  ↓
Refine: "Add Blueprint support" (Quality 94%)
  ↓
Generate Build Files → Done!
```

## 🆘 Getting Help

1. **Check validation tab** - Often shows exactly what's wrong
2. **Review backend logs** - `docker-compose logs backend`
3. **Use Debug mode** - Paste any errors you encounter
4. **Check API docs** - http://localhost:8000/docs (when backend running)

## 🎉 You're Ready!

Start with a simple generation:
```
Mode: Generate
Prompt: "Create a simple Actor with a static mesh component"
```

Then explore the other modes as you get comfortable!

## 📚 Additional Resources

- **Backend API Docs**: http://localhost:8000/docs
- **Original Platform**: See `cpp-ai-automation/README.md`
- **Engine Compatibility**: See `docs/ENGINE_COMPATIBILITY.md`
- **Error Handling Guide**: See `docs/ERROR_HANDLING.md`
