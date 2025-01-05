# Daily Number Increment

This project automatically increments a number in a file daily and pushes the changes to GitHub using a cron job.

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/username/repository-name.git
cd repository-name
```

### 2. Create Python Virtual Environment
```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Create requirements file (if needed)
pip freeze > requirements.txt
```

### 3. Create Initial Files
```bash
# Create number.txt with initial value
echo "0" > number.txt

# Ensure your Python script (number_increment.py) has execute permissions
chmod +x number_increment.py
```

### 4. GitHub Authentication Setup

#### Option A: Using Personal Access Token (Recommended for Automation)
1. Generate a GitHub Personal Access Token:
   - Go to GitHub → Settings → Developer settings → Personal access tokens
   - Click "Generate new token (classic)"
   - Set description and expiration
   - Select `repo` scope
   - Generate and copy the token

2. Update Git Remote URL:
```bash
git remote set-url origin https://YOUR-TOKEN@github.com/username/repository-name.git
```

### 5. Setup Cron Job
```bash
# Add cron job to run daily at 7 AM
echo "0 7 * * * cd /path/to/your/repo && /path/to/your/repo/venv/bin/python /path/to/your/repo/number_increment.py >> /path/to/your/repo/cron.log 2>&1" | crontab -

# Verify cron job
crontab -l
```

### 6. Test Setup
```bash
# Manual test
cd /path/to/your/repo
./venv/bin/python number_increment.py
```

## File Structure
```
repository-name/
├── venv/
├── number_increment.py
├── number.txt
├── cron.log
└── README.md
```

## Monitoring

### Check Logs
```bash
# View cron log
tail -f cron.log
```

### Check Current Number
```bash
cat number.txt
```

## Troubleshooting

### Common Issues

1. **Cron Job Not Running**
   - Check cron service status
   - Verify file permissions
   - Check cron.log for errors

2. **Git Push Failing**
   - Verify token permissions
   - Check remote URL configuration
   - Ensure proper file paths in cron job

### Useful Commands

```bash
# View cron jobs
crontab -l

# Edit cron jobs
crontab -e

# Remove all cron jobs
crontab -r

# Check Git remote
git remote -v
```

## Security Notes

- Never commit your GitHub token to the repository
- Use absolute paths in cron jobs
- Keep your cron.log file for debugging
- Regularly rotate GitHub tokens
