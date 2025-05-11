# Lazy Atia Shrine 🔥

An automated blockchain transaction sender that periodically calls the `activateStreak(address)` function on the Atia Shrine Proxy contract and automatically verifies the "Pray Atia" quest because I'm too lazy and don't want to lose my streak.

## Features

- **Automated Shrine Activation**: Calls the `activateStreak(address)` function on the Atia Shrine Proxy contract
- **Smart Gas Management**: Optimizes gas usage to prevent overpayment
- **Multiple RPC Fallbacks**: Ensures reliable execution even if primary RPC fails

## Security Features

- **Strong Encryption**: AES-256-GCM with random salt, IV, and authentication tag
- **Secure Storage**: Private key never stored in plain text
- **File Permissions**: Encrypted key file has restricted permissions
- **Password Masking**: Private key input is hidden during entry
- **Comprehensive Logging**: All actions are logged for audit and debugging

## Setup

1. Clone this repository:
   ```
   git clone https://github.com/komiwalnut/lazy-atia-shrine.git
   cd lazy-atia-shrine
   ```

2. Install dependencies:
   ```
   pnpm install
   ```

3. Create a `.env` file based on the example:
   ```
   cp .env.example .env
   ```

4. Edit the `.env` file with your settings:
   - Generate a secure encryption key with:
     ```
     node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
     ```
   - Set your dRPC endpoint (follow instruction in `.env` file you just created)

## Usage

### Testing

To test the script:

1. Install Node.js and pnpm
2. Run in test mode to verify everything works without sending transactions:
   ```
   pnpm run test
   ```

### Running Manually

```
pnpm run dev
```

On first run, you'll be prompted to enter your private key, which will be encrypted and stored securely.

### Production Deployment

Build and run:

```
pnpm build
pnpm start
```

### Setting Up a Cron Job

To run the script automatically at 12:00 PM Philippines time (UTC+8) every day:
1. Find your project's absolute path:
   ```
   pwd
   ```
   This will display something like `/home/ec2-user/lazy-atia-shrine`

2. Find the absolute path to your pnpm executable:
   ```
   which pnpm
   ```
   This will display something like `/usr/local/bin/pnpm`

3. Open the crontab editor:
   ```
   crontab -e
   ```

4. Add the following line (replace with your actual paths from steps 1 and 2):
   ```
   0 4 * * * cd /path/to/lazy-atia-shrine && /path/to/pnpm start >> /path/to/lazy-atia-shrine/cron.log 2>&1
   ```
   Example:
   ```
   0 4 * * * cd /home/ec2-user/lazy-atia-shrine && /usr/local/bin/pnpm start >> /home/ec2-user/lazy-atia-shrine/cron.log 2>&1
   ```
   This will run the script at exactly 12:00 PM Philippines time (4:00 AM UTC) every day.

5. Save and exit the editor:
   - For nano: Press Ctrl+O, then Enter, then Ctrl+X
   - For vim: Press Esc, then type `:wq` and hit Enter

6. Verify your cron job was added:
   ```
   crontab -l
   ```

This will run the script at midnight Philippines time and save all output to `cron.log` in your project directory.
