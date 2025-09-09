# Orvaya Theme - Custom Font Implementation

## Overview
This document records the custom font implementation and other customizations made to the Orvaya Shopify theme. The theme now supports 6 custom fonts with conditional application based on merchant settings.

## Custom Fonts Implemented

### 6 Custom Fonts Available:
1. **Documenta Regular** - Serif font
2. **RENPackaging** - Sans-serif font (Light, Regular, Bold)
3. **Siaga** - Sans-serif font (Light, Regular, Medium, Bold with italic variants)
4. **Suisse Book** - Sans-serif font (Light, Book, SemiBold, Bold)
5. **SuisseIntl** - International variant of Suisse
6. **Victor Serif** - Serif font (Regular and Italic)

## File Structure

### Font Files
```
assets/
├── custom-fonts.css                    # @font-face declarations for all custom fonts
├── DocumentaRegular.woff2             # Documenta font file
├── RENPackaging-*.woff2               # RENPackaging font files (Light, Regular, Bold)
├── RENPackaging-*.woff                # RENPackaging fallback files
├── Siaga-*.woff2                      # Siaga font files (all weights and styles)
├── Suisse*.woff2                      # Suisse font files (all weights)
├── SuisseIntl-Regular.woff2           # SuisseIntl font file
└── VictorSerif-*.woff2                # Victor Serif font files
```

### Configuration Files
```
config/
└── settings_schema.json               # Theme settings with custom font options

snippets/
├── stylesheets.liquid                 # CSS file includes
└── theme-styles-variables.liquid      # CSS variables and custom font logic
```

## Theme Settings

### Typography > Fonts Section
The theme now includes 4 checkbox options with corresponding font selectors:

1. **Body Font**
   - Checkbox: "Apply custom font for body text?"
   - Dropdown: "Custom Body Font" (visible when checkbox is enabled)
   - Options: All 6 custom fonts

2. **Subheading Font**
   - Checkbox: "Apply custom font for subheadings?"
   - Dropdown: "Custom Subheading Font" (visible when checkbox is enabled)
   - Options: All 6 custom fonts

3. **Heading Font**
   - Checkbox: "Apply custom font for headings?"
   - Dropdown: "Custom Heading Font" (visible when checkbox is enabled)
   - Options: All 6 custom fonts

4. **Accent Font**
   - Checkbox: "Apply custom font for accent elements?"
   - Dropdown: "Custom Accent Font" (visible when checkbox is enabled)
   - Options: All 6 custom fonts

## Technical Implementation

### 1. Font Loading
- **File**: `assets/custom-fonts.css`
- **Purpose**: Contains @font-face declarations for all custom fonts
- **Features**: 
  - Uses `font-display: swap` for better performance
  - Includes fallback fonts
  - Handles multiple weights and styles

### 2. CSS Variables Logic
- **File**: `snippets/theme-styles-variables.liquid`
- **Purpose**: Defines CSS variables based on merchant settings
- **Logic**:
  - Checks if custom fonts are enabled via checkboxes
  - Maps selected fonts to proper CSS font-family values
  - Handles SuisseIntl → Suisse mapping
  - Overrides default font variables when custom fonts are enabled

### 3. Font Application
- **Method**: CSS variables override
- **Variables Used**:
  - `--font-body--family` (overridden when custom body font enabled)
  - `--font-subheading--family` (overridden when custom subheading font enabled)
  - `--font-heading--family` (overridden when custom heading font enabled)
  - `--font-accent--family` (overridden when custom accent font enabled)

## How It Works

### Merchant Workflow:
1. Go to **Theme Settings > Typography > Fonts**
2. Check the specific custom font checkbox for any typography level (e.g., "Apply custom font for body text?")
3. Select desired custom font from the dropdown that appears
4. Save settings
5. Custom font is automatically applied across the theme

### Technical Flow:
```
Merchant Settings → Liquid Logic → CSS Variables → Existing Theme CSS → Font Applied
```

## Customization History

### Phase 1: Initial Setup
- ✅ Added 4 checkboxes for custom font application
- ✅ Added 4 select dropdowns for font selection
- ✅ Imported 6 custom fonts from Living Proof repository
- ✅ Created @font-face declarations

### Phase 2: Implementation Fix
- ❌ **Issue**: Initially wrote Liquid code directly in CSS files (incorrect approach)
- ✅ **Solution**: Moved logic to `theme-styles-variables.liquid` following Shopify best practices
- ✅ **Result**: Clean implementation using CSS variables

### Phase 3: Optimization
- ✅ Removed unnecessary `custom-font-application.css` file
- ✅ Integrated font logic into existing theme architecture
- ✅ Used CSS variable overrides instead of duplicate CSS rules

## Files Modified

### New Files Created:
- `assets/custom-fonts.css` - Font declarations
- Font files (6 custom fonts with multiple weights/styles)

### Files Modified:
- `config/settings_schema.json` - Added custom font settings
- `snippets/theme-styles-variables.liquid` - Added custom font logic
- `snippets/stylesheets.liquid` - Added custom-fonts.css include

### Files Removed:
- `assets/custom-font-application.css` - Unnecessary duplicate CSS
- `snippets/custom-font-variables.liquid` - Logic moved to main variables file

## Testing Checklist

### Font Loading:
- [ ] All 6 custom fonts load correctly
- [ ] Font files are properly referenced
- [ ] Fallback fonts work when custom fonts fail

### Theme Settings:
- [ ] Checkboxes appear in Typography > Fonts section
- [ ] Dropdowns only show when checkboxes are enabled
- [ ] All 6 fonts appear in each dropdown
- [ ] Settings save and persist correctly

### Font Application:
- [ ] Body font applies to paragraphs, product cards, etc.
- [ ] Subheading font applies to subheading elements
- [ ] Heading font applies to h1-h6, titles, etc.
- [ ] Accent font applies to buttons, badges, etc.
- [ ] Fonts only apply when checkboxes are enabled
- [ ] Default fonts work when custom fonts are disabled

## Future Enhancements

### Potential Improvements:
1. **Font Weight Options**: Add weight selection for each custom font
2. **Font Size Scaling**: Custom size adjustments for custom fonts
3. **Font Pairing Suggestions**: Predefined font combinations
4. **Preview Mode**: Live preview of font changes in theme editor
5. **Additional Fonts**: Import more fonts from other sources

### Maintenance Notes:
- Font files are stored in `assets/` directory
- CSS variables are defined in `theme-styles-variables.liquid`
- Settings are configured in `settings_schema.json`
- Always test font loading and application after changes

## Troubleshooting

### Common Issues:
1. **Fonts not loading**: Check file paths in `custom-fonts.css`
2. **Fonts not applying**: Verify CSS variables are being overridden
3. **Settings not saving**: Check `settings_schema.json` syntax
4. **Performance issues**: Ensure `font-display: swap` is used

### Debug Steps:
1. Check browser developer tools for font loading errors
2. Verify CSS variables in theme-styles-variables.liquid
3. Test with different font combinations
4. Check theme settings in Shopify admin

---

**Last Updated**: December 2024  
**Version**: 1.0  
**Status**: Complete and Functional
