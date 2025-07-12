# Custom Icons Guide

This guide explains how to create and use custom icons in the Roblox Friend Viewer application.

## Current Icon System

The application uses SVG icons for verification and premium badges located in:
- `client/src/assets/icons/verified.svg` - Blue checkmark for verified users
- `client/src/assets/icons/premium.svg` - Golden star for premium users

## Creating Custom Icons

### 1. Design Guidelines

**SVG Format Requirements:**
- Use SVG format for scalability and crisp display
- Recommended size: 20x20 pixels viewBox
- Keep file size under 5KB for optimal performance
- Use inline styles or CSS classes for colors

**Design Specifications:**
- **Verified Badge**: Blue theme (#1D4ED8), checkmark or shield design
- **Premium Badge**: Gold/yellow theme (#F59E0B), star or crown design
- **Custom Badges**: Use distinctive colors and shapes

### 2. Creating Your Icons

#### Option A: Design Tools
1. **Adobe Illustrator**: Create 20x20px artboard, design icon, export as SVG
2. **Figma**: Create 20x20px frame, design icon, export as SVG
3. **Inkscape** (Free): Create 20x20px document, design icon, save as SVG

#### Option B: Online Tools
1. **Heroicons**: Browse free SVG icons at heroicons.com
2. **Lucide**: Browse icons at lucide.dev
3. **Tabler Icons**: Browse at tabler-icons.io

### 3. SVG Code Structure

Here's the structure for a custom icon:

```svg
<svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
  <!-- Your icon paths here -->
  <path d="..." fill="#YOUR_COLOR"/>
  <!-- Add gradients if needed -->
  <defs>
    <linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" style="stop-color:#COLOR1;stop-opacity:1" />
      <stop offset="100%" style="stop-color:#COLOR2;stop-opacity:1" />
    </linearGradient>
  </defs>
</svg>
```

### 4. Adding Icons to the Application

#### Step 1: Save Your Icon
1. Save your SVG file in `client/src/assets/icons/`
2. Use descriptive names: `admin.svg`, `moderator.svg`, `vip.svg`

#### Step 2: Import in Component
Edit `client/src/components/special-tag.tsx`:

```typescript
import adminIcon from "@/assets/icons/admin.svg";
import moderatorIcon from "@/assets/icons/moderator.svg";
```

#### Step 3: Create Badge Component
Add a new badge component:

```typescript
export function AdminBadge() {
  return (
    <img 
      src={adminIcon} 
      alt="Admin" 
      className="w-5 h-5 inline-block"
      title="Admin User"
    />
  );
}
```

#### Step 4: Use in Profile/Friend Cards
Add to user profile or friend card components:

```typescript
{user.isAdmin && <AdminBadge />}
```

## Icon Examples

### Verification Badge (Current)
```svg
<svg width="20" height="20" viewBox="0 0 20 20" fill="none">
<path d="M10 0L12.2451 2.24514L15.8779 1.90983L16.9098 5.12215L20 6.90983L18.7549 10L20 13.0902L16.9098 14.8779L15.8779 18.0902L12.2451 17.7549L10 20L7.75486 17.7549L4.12215 18.0902L3.09017 14.8779L0 13.0902L1.24514 10L0 6.90983L3.09017 5.12215L4.12215 1.90983L7.75486 2.24514L10 0Z" fill="#1D4ED8"/>
<path d="M14 7L8.5 12.5L6 10" stroke="white" stroke-width="2"/>
</svg>
```

### Admin Badge (Example)
```svg
<svg width="20" height="20" viewBox="0 0 20 20" fill="none">
<path d="M10 2L12 6H16L13 9L14 13L10 11L6 13L7 9L4 6H8L10 2Z" fill="#DC2626"/>
<circle cx="10" cy="10" r="2" fill="white"/>
</svg>
```

## Color Palette

**Recommended colors for different badge types:**
- **Verified**: `#1D4ED8` (Blue)
- **Premium**: `#F59E0B` (Gold)
- **Admin**: `#DC2626` (Red)
- **Moderator**: `#7C3AED` (Purple)
- **VIP**: `#EC4899` (Pink)
- **Developer**: `#059669` (Green)

## Integration with Special Tags System

The application uses a special tags system in `special-tags.json`. To integrate custom icons:

1. Add your user ID to `special-tags.json`
2. Create corresponding badge components
3. Update the display logic in `special-tag.tsx`

Example `special-tags.json` entry:
```json
{
  "123456789": {
    "tag": "ADMIN",
    "color": "#DC2626",
    "animated": true
  }
}
```

## Best Practices

1. **Consistency**: Use similar design language across all custom icons
2. **Accessibility**: Include meaningful `alt` text and `title` attributes
3. **Performance**: Optimize SVGs to reduce file size
4. **Scalability**: Test icons at different sizes (16px, 20px, 24px)
5. **Contrast**: Ensure icons are visible on dark backgrounds

## Troubleshooting

**Icons not displaying:**
- Check file path in import statement
- Verify SVG syntax is valid
- Ensure file is in correct directory

**Icons appear corrupted:**
- Check SVG viewBox dimensions
- Verify all paths are closed properly
- Remove any invalid attributes

**Icons too large/small:**
- Adjust `className="w-5 h-5"` values
- Check SVG viewBox matches content

## Support

For additional help with custom icons, refer to:
- SVG specification: https://developer.mozilla.org/en-US/docs/Web/SVG
- SVG optimization: https://jakearchibald.github.io/svgomg/