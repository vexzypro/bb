# Fragments & Artifacts Resource Pack

A complete Minecraft Java Edition resource pack (version 1.21.x, pack_format 34) providing vibrant, glowing tile-style HUD icons and custom item models for a fragments & artifacts plugin.

## Features

- **HUD Icons**: 16 vibrant, glowing icons displayed above the hotbar using bitmap font glyphs
- **Custom Item Models**: Custom textures for 8 artifact fragments and 8 artifacts via Custom Model Data
- **Base Item**: All custom items use `paper` as the base item
- **Style**: Bright, saturated tiles with thick borders, inner glow, and soft outer rim glow

## Installation

1. Download or clone this resource pack
2. Place the entire folder in your Minecraft `resourcepacks` directory:
   - Windows: `%appdata%\.minecraft\resourcepacks\`
   - macOS: `~/Library/Application Support/minecraft/resourcepacks/`
   - Linux: `~/.minecraft/resourcepacks/`
3. Launch Minecraft 1.21.x
4. Go to Options → Resource Packs
5. Select "Fragments & Artifacts HUD + item models (1.21.x)"
6. Click "Done"

## Glyph Mapping (HUD Icons)

Use these Unicode characters in ActionBar messages or other text components to display HUD icons above the hotbar:

### Fragments (Row 1 & 2)
| Glyph | Unicode | Name | Description |
|-------|---------|------|-------------|
| 🔥 | `\uE001` | Fire Fragment | Bright orange-red flame icon |
| 💨 | `\uE002` | Wind Fragment | Cyan wind/air icon |
| ⚡ | `\uE003` | Zeus Fragment | Bright yellow lightning icon |
| 🌀 | `\uE004` | Ender Fragment | Purple void/portal icon |
| 👁️ | `\uE005` | Vision Fragment | Teal eye/vision icon |
| 💪 | `\uE006` | Strength Fragment | Pink-red power icon |
| 🧠 | `\uE007` | Telekinesis Fragment | Blue-purple mind icon |
| 🌊 | `\uE008` | Poseidon Fragment | Ocean blue water icon |

### Artifacts (Row 3 & 4)
| Glyph | Unicode | Name | Description |
|-------|---------|------|-------------|
| 🔥 | `\uE009` | Fire Artifact | Enhanced fire icon |
| 💨 | `\uE00A` | Wind Artifact | Enhanced wind icon |
| ⚡ | `\uE00B` | Zeus Artifact | Enhanced lightning icon |
| 🌀 | `\uE00C` | Ender Artifact | Enhanced void icon |
| 👁️ | `\uE00D` | Vision Artifact | Enhanced vision icon |
| 💪 | `\uE00E` | Strength Artifact | Enhanced strength icon |
| 🧠 | `\uE00F` | Telekinesis Artifact | Enhanced telekinesis icon |
| 🌊 | `\uE010` | Poseidon Artifact | Enhanced water icon |

## Custom Model Data Mapping

Use these CMD values when giving items to players:

### Fragments (CMD 1001-1008)
| Item | CMD | Command Example |
|------|-----|-----------------|
| Fire Fragment | 1001 | `/give @p paper{CustomModelData:1001} 1` |
| Wind Fragment | 1002 | `/give @p paper{CustomModelData:1002} 1` |
| Zeus Fragment | 1003 | `/give @p paper{CustomModelData:1003} 1` |
| Ender Fragment | 1004 | `/give @p paper{CustomModelData:1004} 1` |
| Vision Fragment | 1005 | `/give @p paper{CustomModelData:1005} 1` |
| Strength Fragment | 1006 | `/give @p paper{CustomModelData:1006} 1` |
| Telekinesis Fragment | 1007 | `/give @p paper{CustomModelData:1007} 1` |
| Poseidon Fragment | 1008 | `/give @p paper{CustomModelData:1008} 1` |

### Artifacts (CMD 1011-1018)
| Item | CMD | Command Example |
|------|-----|-----------------|
| Fire Artifact | 1011 | `/give @p paper{CustomModelData:1011} 1` |
| Wind Artifact | 1012 | `/give @p paper{CustomModelData:1012} 1` |
| Zeus Artifact | 1013 | `/give @p paper{CustomModelData:1013} 1` |
| Ender Artifact | 1014 | `/give @p paper{CustomModelData:1014} 1` |
| Vision Artifact | 1015 | `/give @p paper{CustomModelData:1015} 1` |
| Strength Artifact | 1016 | `/give @p paper{CustomModelData:1016} 1` |
| Telekinesis Artifact | 1017 | `/give @p paper{CustomModelData:1017} 1` |
| Poseidon Artifact | 1018 | `/give @p paper{CustomModelData:1018} 1` |

## Usage Examples

### ActionBar HUD Display (Bukkit/Spigot/Paper)

```java
import net.md_5.bungee.api.ChatMessageType;
import net.md_5.bungee.api.chat.TextComponent;
import org.bukkit.entity.Player;

public class ArtifactHUD {
    
    // Display a single icon in the ActionBar
    public static void showIcon(Player player, String unicode) {
        player.spigot().sendMessage(ChatMessageType.ACTION_BAR, 
            new TextComponent(unicode));
    }
    
    // Display multiple icons (e.g., collected fragments)
    public static void showFragments(Player player, boolean[] hasFragment) {
        StringBuilder hud = new StringBuilder();
        
        // Add spacing for centering
        hud.append("    ");
        
        // Fragment glyphs in order
        String[] glyphs = {
            "\uE001", // Fire
            "\uE002", // Wind
            "\uE003", // Zeus
            "\uE004", // Ender
            "\uE005", // Vision
            "\uE006", // Strength
            "\uE007", // Telekinesis
            "\uE008"  // Poseidon
        };
        
        for (int i = 0; i < glyphs.length; i++) {
            if (hasFragment[i]) {
                hud.append(glyphs[i]);
            } else {
                hud.append(" "); // Empty space for missing fragment
            }
            hud.append(" "); // Spacing between icons
        }
        
        player.spigot().sendMessage(ChatMessageType.ACTION_BAR, 
            new TextComponent(hud.toString()));
    }
    
    // Display artifact status
    public static void showArtifacts(Player player, int activeArtifact) {
        String[] artifactGlyphs = {
            "\uE009", // Fire Artifact
            "\uE00A", // Wind Artifact
            "\uE00B", // Zeus Artifact
            "\uE00C", // Ender Artifact
            "\uE00D", // Vision Artifact
            "\uE00E", // Strength Artifact
            "\uE00F", // Telekinesis Artifact
            "\uE010"  // Poseidon Artifact
        };
        
        if (activeArtifact >= 0 && activeArtifact < artifactGlyphs.length) {
            String message = "    Active: " + artifactGlyphs[activeArtifact];
            player.spigot().sendMessage(ChatMessageType.ACTION_BAR, 
                new TextComponent(message));
        }
    }
}
```

### Giving Items with Custom Model Data

```java
import org.bukkit.Material;
import org.bukkit.inventory.ItemStack;
import org.bukkit.inventory.meta.ItemMeta;

public class ArtifactItems {
    
    public static ItemStack createFragment(String type) {
        ItemStack item = new ItemStack(Material.PAPER);
        ItemMeta meta = item.getItemMeta();
        
        // Set Custom Model Data based on fragment type
        switch (type.toLowerCase()) {
            case "fire":
                meta.setCustomModelData(1001);
                meta.setDisplayName("§c§lFire Fragment");
                break;
            case "wind":
                meta.setCustomModelData(1002);
                meta.setDisplayName("§b§lWind Fragment");
                break;
            case "zeus":
                meta.setCustomModelData(1003);
                meta.setDisplayName("§e§lZeus Fragment");
                break;
            case "ender":
                meta.setCustomModelData(1004);
                meta.setDisplayName("§5§lEnder Fragment");
                break;
            case "vision":
                meta.setCustomModelData(1005);
                meta.setDisplayName("§3§lVision Fragment");
                break;
            case "strength":
                meta.setCustomModelData(1006);
                meta.setDisplayName("§d§lStrength Fragment");
                break;
            case "telekinesis":
                meta.setCustomModelData(1007);
                meta.setDisplayName("§9§lTelekinesis Fragment");
                break;
            case "poseidon":
                meta.setCustomModelData(1008);
                meta.setDisplayName("§1§lPoseidon Fragment");
                break;
        }
        
        item.setItemMeta(meta);
        return item;
    }
    
    public static ItemStack createArtifact(String type) {
        ItemStack item = new ItemStack(Material.PAPER);
        ItemMeta meta = item.getItemMeta();
        
        // Set Custom Model Data based on artifact type
        switch (type.toLowerCase()) {
            case "fire":
                meta.setCustomModelData(1011);
                meta.setDisplayName("§c§l§nFire Artifact");
                break;
            case "wind":
                meta.setCustomModelData(1012);
                meta.setDisplayName("§b§l§nWind Artifact");
                break;
            case "zeus":
                meta.setCustomModelData(1013);
                meta.setDisplayName("§e§l§nZeus Artifact");
                break;
            case "ender":
                meta.setCustomModelData(1014);
                meta.setDisplayName("§5§l§nEnder Artifact");
                break;
            case "vision":
                meta.setCustomModelData(1015);
                meta.setDisplayName("§3§l§nVision Artifact");
                break;
            case "strength":
                meta.setCustomModelData(1016);
                meta.setDisplayName("§d§l§nStrength Artifact");
                break;
            case "telekinesis":
                meta.setCustomModelData(1017);
                meta.setDisplayName("§9§l§nTelekinesis Artifact");
                break;
            case "poseidon":
                meta.setCustomModelData(1018);
                meta.setDisplayName("§1§l§nPoseidon Artifact");
                break;
        }
        
        item.setItemMeta(meta);
        return item;
    }
}
```

## Resource Pack Structure

```
├── pack.mcmeta
├── assets/
│   └── minecraft/
│       ├── font/
│       │   └── default.json
│       ├── models/
│       │   └── item/
│       │       ├── paper.json
│       │       └── artifacts/
│       │           ├── fire_fragment.json
│       │           ├── wind_fragment.json
│       │           ├── zeus_fragment.json
│       │           ├── ender_fragment.json
│       │           ├── vision_fragment.json
│       │           ├── strength_fragment.json
│       │           ├── telekinesis_fragment.json
│       │           ├── poseidon_fragment.json
│       │           ├── fire_artifact.json
│       │           ├── wind_artifact.json
│       │           ├── zeus_artifact.json
│       │           ├── ender_artifact.json
│       │           ├── vision_artifact.json
│       │           ├── strength_artifact.json
│       │           ├── telekinesis_artifact.json
│       │           └── poseidon_artifact.json
│       └── textures/
│           ├── font/
│           │   └── artifacts_icons.png (128x128 spritesheet)
│           └── item/
│               └── artifacts/
│                   ├── fire_fragment.png
│                   ├── wind_fragment.png
│                   ├── zeus_fragment.png
│                   ├── ender_fragment.png
│                   ├── vision_fragment.png
│                   ├── strength_fragment.png
│                   ├── telekinesis_fragment.png
│                   ├── poseidon_fragment.png
│                   ├── fire_artifact.png
│                   ├── wind_artifact.png
│                   ├── zeus_artifact.png
│                   ├── ender_artifact.png
│                   ├── vision_artifact.png
│                   ├── strength_artifact.png
│                   ├── telekinesis_artifact.png
│                   └── poseidon_artifact.png
```

## Technical Details

- **Pack Format**: 34 (Minecraft 1.21.x)
- **Font Provider**: Bitmap font at `minecraft:font/artifacts_icons.png`
- **Icon Size**: 32x32 pixels per icon
- **Spritesheet**: 128x128 pixels (4x4 grid)
- **Ascent**: 31 (positions icons above hotbar)
- **Height**: 32 (icon display height)
- **Base Item**: Paper (can be changed by editing model files)

## Customization

### Changing Colors
To change icon colors, edit the Python generation script or use an image editor to modify:
- `assets/minecraft/textures/font/artifacts_icons.png` (HUD spritesheet)
- `assets/minecraft/textures/item/artifacts/*.png` (individual item textures)

### Changing Base Item
To use a different base item instead of paper:
1. Rename `assets/minecraft/models/item/paper.json` to the desired item (e.g., `diamond.json`)
2. Update the `layer0` texture in the renamed file
3. Update all `/give` commands to use the new base item

### Adding More Icons
1. Edit `assets/minecraft/font/default.json` to add more Unicode characters
2. Expand the spritesheet or create a new one
3. Add corresponding model and texture files

## Compatibility

- **Minecraft Version**: 1.21.x (Java Edition)
- **Server Software**: Bukkit, Spigot, Paper, Purpur, or any fork
- **Required**: Server must support Custom Model Data (1.14+)
- **Client**: Players must have this resource pack installed

## License

This resource pack is provided as-is for use with Minecraft servers.

## Credits

Created for the Fragments & Artifacts plugin system.
