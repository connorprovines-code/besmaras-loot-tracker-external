# Besmara's Loot Tracker 🏴‍☠️

A real-time collaborative loot tracker for Pathfinder 1e pirate campaigns. Track party gold, crew wages, and inventory with instant synchronization across multiple users.

![Pathfinder 1e](https://img.shields.io/badge/Pathfinder-1e-blue)
![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)
![Supabase](https://img.shields.io/badge/Supabase-Realtime-3ECF8E?logo=supabase)
![License](https://img.shields.io/badge/License-MIT-green)

## Features

### 📦 Loot Management
- **Incoming Loot**: Add items as you find them
- **Treasure vs Loot**: Treasure sells at 100%, loot at 50%
- **Bulk Import**: Paste formatted loot lists for quick entry
- **Smart Assignment**: Assign items to players or party fund
- **Sell & Distribute**: Automatically split gold among party members

### 💰 Gold Tracking
- **Individual Player Gold**: Track each player's wealth
- **Party Fund**: Shared gold pool for group expenses
- **Transaction Log**: Complete history of all gold movements
- **Manual Adjustments**: Edit gold values with automatic logging

### 👥 Crew Management
- **Level-Based Tracking**: Manage crew levels 1-10
- **Automatic Wage Calculation**: (5gp × Level)² + 9gp food per crew
- **Pay Wages Button**: Deduct from party fund with one click
- **Transaction Logging**: All wage payments recorded

### 🎒 Inventory System
- **Per-Player Inventories**: Each player has their own inventory
- **Party Inventory**: Shared party items
- **Item Transfer**: Move items between players
- **Consumables Tab**: Track items with charges
- **Charge Tracking**: Increment/decrement item charges

### ⚡ Real-Time Collaboration
- **Live Updates**: See changes instantly across all users
- **Multi-User Support**: 2-10+ players simultaneously
- **Automatic Sync**: Items, gold, crew, transactions all sync in real-time
- **Conflict Prevention**: Database constraints prevent data corruption

## Quick Start

### 1. Prerequisites
- Node.js 18+ installed
- A Supabase account (free tier works great!)

### 2. Clone & Install
```bash
git clone https://github.com/connorprovines-code/besmaras-loot-tracker-external.git
cd besmaras-loot-tracker-external
npm install
```

### 3. Set Up Supabase

#### Create a Supabase Project
1. Go to [supabase.com](https://supabase.com)
2. Create a new project
3. Go to **Settings** → **API**
4. Copy your **Project URL** and **anon public key**

#### Create Environment File
```bash
cp .env.example .env
```

Edit `.env` and add your credentials:
```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

#### Run Database Setup
1. In Supabase, go to **SQL Editor**
2. Run the SQL from `database_setup.sql` (creates tables)
3. Run the SQL from `database_constraints.sql` (enables real-time + constraints)

### 4. Start Development Server
```bash
npm run dev
```

Visit `http://localhost:5173` 🎉

## Database Schema

The app creates these tables:

- **players**: Player names and gold amounts
- **party_fund**: Shared party gold
- **items**: All loot items (incoming, assigned, sold, etc.)
- **transactions**: Complete transaction history
- **crew**: Crew counts by level (JSON)

See `database_setup.sql` for full schema.

## Real-Time Setup

Real-time collaboration is **enabled by default**. To use it:

1. Run `database_constraints.sql` in Supabase (critical for data protection)
2. Open the app in multiple browsers
3. Changes sync automatically!

### Kill Switch
To disable real-time, edit `src/App.jsx`:
```javascript
const ENABLE_REALTIME = false; // Change to false
```

See `REALTIME_SETUP.md` for detailed documentation.

## Deployment

### Vercel (Recommended)
1. Push to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Import your repository
4. Add environment variables:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
5. Deploy!

### Netlify
```bash
npm run build
# Drag and drop the `dist` folder to Netlify
```

## Configuration

### Crew Wage Formula
The wage calculation is: **(5gp × Level)² + 9gp food per crew**

Example costs per crew member per month:
- Level 1: 34 gp
- Level 5: 634 gp
- Level 10: 2,509 gp

### Gold Distribution
When selling loot:
- Treasure: 100% of value
- Loot: 50% of value
- Split evenly: Players + Party Fund

## Usage Tips

### Adding Players
1. Go to **Settings** tab
2. Click **Add Player**
3. Players start with 0 gp

### Managing Loot
1. Add items in **Incoming Loot**
2. Mark as "Treasure" if it sells at full value
3. Either **Sell** (distribute gold) or **Assign** to a player
4. Assigned items go to player inventories

### Paying Crew Wages
1. Go to **Crew** tab
2. Adjust crew counts with +/- buttons
3. Click **Pay Wages**
4. Confirm payment (deducts from Party Fund)

### Bulk Import
Format: `* [quantity] [item name] = [price per unit] gp`
```
* 4 mwk breastplate = 700 gp
* 10 crossbow bolts = 0.5 gp
* 1 spellbook = 7.5 gp
```

## Tech Stack

- **Frontend**: React 18 + Vite
- **Styling**: Tailwind CSS
- **Backend**: Supabase (PostgreSQL)
- **Real-Time**: Supabase Realtime (WebSockets)
- **Icons**: Lucide React

## Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Troubleshooting

### Real-Time Not Working?
- ✓ Run `database_constraints.sql`
- ✓ Check Supabase Realtime is enabled
- ✓ Verify `ENABLE_REALTIME = true`
- ✓ Check browser console for errors

### Database Errors?
- ✓ Run `database_setup.sql` first
- ✓ Check Row Level Security policies
- ✓ Verify environment variables are set

### Build Errors?
```bash
rm -rf node_modules package-lock.json
npm install
npm run build
```

## License

MIT License - feel free to use this for your own campaigns!

## Credits

Built for Pathfinder 1e pirate campaigns, inspired by the Skull & Shackles Adventure Path.

**Besmara's blessing upon your plunder!** 🏴‍☠️⚔️💰

---

## Links

- [Live Demo](https://your-demo-url-here.vercel.app) (Coming Soon)
- [Issue Tracker](https://github.com/connorprovines-code/besmaras-loot-tracker-external/issues)
- [Supabase](https://supabase.com)
- [Pathfinder 1e SRD](https://www.d20pfsrd.com)
