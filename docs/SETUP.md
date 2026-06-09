# Setup Guide

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js**: Version 18.0.0 or higher ([Download](https://nodejs.org/))
- **pnpm**: Version 8.0.0 or higher (`npm install -g pnpm`)
- **Git**: For version control ([Download](https://git-scm.com/))
- **Docker** (Optional): For local PostgreSQL and Redis ([Download](https://www.docker.com/))
- **A Supabase Account**: Free tier available at [supabase.com](https://supabase.com/)

## Step 1: Clone the Repository

```bash
git clone https://github.com/PCLSADMIN/nexus-platform-core.git
cd nexus-platform-core
```

## Step 2: Install Dependencies

```bash
pnpm install
```

This will install dependencies for the entire monorepo structure.

## Step 3: Set Up Supabase

### Option A: Using Supabase Cloud

1. Create a free account at [supabase.com](https://supabase.com/)
2. Create a new project
3. In the project settings, copy:
   - Project URL → `NEXT_PUBLIC_SUPABASE_URL`
   - Anon Public Key → `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - Service Role Secret → `SUPABASE_SERVICE_ROLE_KEY`

### Option B: Using Local Supabase (Docker)

1. Ensure Docker is running
2. Start the local Supabase stack:
   ```bash
   docker-compose up -d postgres redis
   ```

## Step 4: Configure Environment Variables

1. Copy the example environment file:
   ```bash
   cp .env.example .env.local
   cp apps/web/.env.local.example apps/web/.env.local
   ```

2. Edit `.env.local` with your Supabase credentials:
   ```env
   NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key_here
   SUPABASE_SERVICE_ROLE_KEY=your_service_role_key_here
   ```

3. For database access, set optional variables:
   ```env
   DATABASE_URL=postgresql://user:password@localhost:5432/nexus_platform
   ```

## Step 5: Initialize the Database

### Option A: With Supabase Cloud

1. Go to your Supabase project dashboard
2. Go to SQL Editor → Create new query
3. Copy and run the SQL from `supabase/schema.sql`

### Option B: With Local Database

```bash
# Run migrations
pnpm db:migrate

# Seed the database (optional)
pnpm db:seed
```

## Step 6: Start Development Server

```bash
pnpm dev
```

The application will be available at `http://localhost:3000`

## Verification

1. Open [http://localhost:3000](http://localhost:3000) in your browser
2. You should see the application home page
3. Try logging in with the test credentials (if seeded)

## Troubleshooting

### Port Already in Use

If port 3000 is already in use:

```bash
# Use a different port
pnpm dev -- -p 3001
```

### Supabase Connection Issues

1. Verify environment variables are set correctly:
   ```bash
   echo $NEXT_PUBLIC_SUPABASE_URL
   echo $NEXT_PUBLIC_SUPABASE_ANON_KEY
   ```

2. Check Supabase project is active in the dashboard

3. Ensure your IP is not blocked by Supabase firewall

### Database Migration Issues

1. Check database connection:
   ```bash
   pnpm db:migrate --verbose
   ```

2. Verify SQL syntax in `supabase/schema.sql`

3. Check database logs in Supabase dashboard

### Node Modules Issues

```bash
# Clear and reinstall
pnpm clean:all
pnpm install
```

## Development Tools

### Code Editor Setup (VS Code)

1. Install recommended extensions:
   - ESLint
   - Prettier - Code formatter
   - TypeScript Vue Plugin (Volar)
   - Tailwind CSS IntelliSense

2. Create `.vscode/settings.json`:
   ```json
   {
     "editor.formatOnSave": true,
     "editor.defaultFormatter": "esbenp.prettier-vscode",
     "[typescript]": {
       "editor.defaultFormatter": "esbenp.prettier-vscode"
     }
   }
   ```

### Database Management

View and manage your database:

```bash
# Open Supabase Studio
pnpm db:studio

# Or use the web dashboard at your Supabase project URL
```

## Next Steps

1. **Read the Documentation**: See `/docs` for detailed guides
2. **Explore the Codebase**: Familiarize yourself with the project structure
3. **Run Tests**: `pnpm test` to ensure everything is working
4. **Start Contributing**: See [CONTRIBUTING.md](../CONTRIBUTING.md)

## Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Supabase Documentation](https://supabase.com/docs)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [React Documentation](https://react.dev)

## Common Commands Reference

```bash
# Development
pnpm dev              # Start dev server
pnpm build            # Production build
pnpm start            # Start production server
pnpm lint             # Check code quality
pnpm format           # Format code
pnpm type-check       # TypeScript check

# Testing
pnpm test             # Run tests
pnpm test:watch       # Watch mode
pnpm test:coverage    # Coverage report
pnpm test:e2e         # E2E tests

# Database
pnpm db:migrate       # Run migrations
pnpm db:seed          # Seed database
pnpm db:reset         # Reset database
pnpm db:studio        # Open Supabase Studio
```

## Getting Help

- 💬 [GitHub Discussions](https://github.com/PCLSADMIN/nexus-platform-core/discussions)
- 🐛 [Report Issues](https://github.com/PCLSADMIN/nexus-platform-core/issues)
- 📧 Email: support@nexus-platform.com

---

**Last Updated**: June 2026
