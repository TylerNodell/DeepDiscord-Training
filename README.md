# DeepDiscord Training

Complete AI model training infrastructure for Discord personality bots. Supports local training, OpenAI fine-tuning, and Together.ai cloud training.

## 🏗️ Project Structure

```
DeepDiscord/
├── discord_bot/           # Complete Discord bot system
│   ├── discord_bot.py     # Main bot with MessageTracker
│   ├── enhanced_commands.py # Advanced bot commands
│   ├── tools/             # Bot-specific utilities
│   │   ├── training_data_generator.py # Extract training data
│   │   └── enhanced_message_tracker.py # Advanced tracking logic
│   ├── scripts/           # Bot convenience scripts
│   │   ├── run_tests.sh   # Run test suite
│   │   └── generate_training_data.sh # Generate training data
│   ├── tests/             # Bot test suite
│   └── results/           # Generated training data archives
├── training_module/       # AI model training infrastructure
│   ├── config/            # Training configuration management
│   ├── models/            # Model architectures and training
│   ├── data/              # Data loading and preprocessing
│   ├── utils/             # Training utilities
│   ├── scripts/           # Training and evaluation scripts
│   ├── experiments/       # Experiment tracking
│   └── checkpoints/       # Model saves and checkpoints
├── docs/                  # Documentation and research
└── results/              # Shared training data outputs
```

## 🎯 Features

### 🤖 Core Bot Functionality
- **Message Fragment Detection**: Automatically combines rapid-fire messages from the same user
- **Response Chain Tracking**: Tracks explicit replies using Discord's reference system  
- **User Message Analysis**: Comprehensive analysis of user communication patterns
- **Real-time Processing**: Live message tracking and analysis

### 🎓 Training Data Generation
- **Question/Answer Pair Extraction**: Generate training data from Discord conversations
- **Multiple Confidence Levels**: High, medium, and all response pairs
- **Smart Response Detection**: Temporal proximity, content analysis, and explicit replies
- **Fragment Integration**: Includes combined fragmented messages in training data

### 📊 Analytics & Insights
- **User Communication Patterns**: Fragment detection, response rates, activity analysis
- **Conversation Flow Analysis**: Identify standalone messages vs responses
- **Historical Data Processing**: Analyze past conversations for insights

## 🚀 Quick Start

### 1. Setup
```bash
# Clone and setup environment
git clone <repository>
cd DeepDiscord
cp .env.example .env
# Edit .env with your Discord bot token and target user ID
```

### 2. Run Tests
```bash
# Test Discord connectivity and user analysis
./discord_bot/scripts/run_tests.sh

# Or run specific test
./discord_bot/scripts/run_tests.sh test_discord_user.py
```

### 3. Generate Training Data
```bash
# Generate question/answer pairs for training
./discord_bot/scripts/generate_training_data.sh
```

### 4. Run Discord Bot
```bash
python discord_bot/discord_bot.py
```

## Configuration

### Environment Variables (`.env`)
```bash
# Required
DISCORD_TOKEN=your_discord_bot_token_here
TEST_USER_ID=123456789012345678

# Optional
BOT_PREFIX=!!
LOG_LEVEL=INFO
```

## Usage Examples

### Generate Training Data
```bash
# Generate training pairs for the user specified in .env
python discord_bot/tools/training_data_generator.py

# Output files (now in ZIP format):
# discord_bot/results/training_data_<username>_<timestamp>.zip
# Contains: high_confidence, medium_confidence, and all_responses JSON files
```

### Training Data Format
```json
{
  "question": "OtherUser: What's your favorite game?",
  "answer": "I really love Final Fantasy XIV, been playing for years!",
  "metadata": {
    "response_type": "temporal_proximity",
    "confidence": 0.85,
    "channel": "general",
    "timestamp": "2025-01-19T12:34:56"
  }
}
```

### Bot Commands
```bash
!!userhistory @user                    # Analyze user's message patterns
!!fragment @user                       # Show fragment detection results  
!!relationships @user                  # Show message relationships
!!generatetrainingdata <user_id> [days] # Generate training data files for specific user
!!consent                              # Check your consent status
!!consent status [@user]               # Check consent status (self or others)
!!consent grant @user                  # Grant consent to someone
!!consent revoke                       # Revoke your consent
```

#### Training Data Generation
The `!!generatetrainingdata` command creates question/answer training pairs from Discord conversations:

```bash
# Generate training data for user (30 days default)
!!generatetrainingdata 123456789012345678

# Generate training data for user (60 days back)
!!generatetrainingdata 123456789012345678 60
```

**Features:**
- **Smart timeout management**: Processes large histories without Discord API timeouts
- **Multiple confidence levels**: Generates high, medium, and all confidence datasets
- **Real-time status updates**: Shows progress with live message counts
- **Automatic file delivery**: Uploads JSON files directly to Discord
- **Fragment integration**: Includes combined fragmented messages in training data

#### 🔒 Privacy & Consent System
DeepDiscord includes a comprehensive consent system that protects user privacy:

**How it works:**
1. When someone runs `!!generatetrainingdata` for a user
2. If the user hasn't given consent, they receive a DM with a detailed request
3. Users can accept (✅) or decline (❌) via reaction
4. Only with explicit consent will data collection proceed

**Consent Management:**
```bash
# Check your consent status
!!consent

# Check someone else's consent status  
!!consent status @username

# Grant consent to someone (if they asked you directly)
!!consent grant @requester

# Revoke your consent anytime
!!consent revoke
```

**Privacy Protections:**
- **Explicit consent required**: No data collection without user permission
- **Detailed disclosure**: Users see exactly what data will be collected
- **Time-limited**: Consent expires after 90 days
- **Revocable**: Users can withdraw consent anytime
- **Transparent**: Clear audit trail of all consent activities
- **DM notifications**: Users are notified of requests and decisions

## AI Training Module

The `training_module/` directory contains a complete infrastructure for training AI models on Discord conversation data.

### Features
- **Configuration-driven training** with flexible hyperparameters
- **Data preprocessing pipeline** for Discord training archives
- **Multiple model architectures** support
- **Experiment tracking** and checkpoint management
- **Comprehensive evaluation** metrics and testing

### Quick Start
```bash
# Install training dependencies
pip install -r training_module/requirements.txt

# Configure training parameters
# Edit training_module/config/training_config.py

# Preprocess Discord training data
python training_module/scripts/preprocess_data.py

# Train the model
python training_module/scripts/train.py

# Evaluate model performance
python training_module/scripts/evaluate.py
```

See `training_module/README.md` for detailed documentation.

## Development

### Running Tests
```bash
# Full test suite
./discord_bot/scripts/run_tests.sh

# Individual tests
python discord_bot/tests/test_discord_user.py
python discord_bot/tests/test_specific_features.py
```

### Adding Features
1. Create feature branch from main
2. Implement in `discord_bot/` for bot features or `training_module/` for AI training
3. Add tests in respective `tests/` directories
4. Update documentation

## License

MIT License - see LICENSE file for details.
