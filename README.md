# Stratego 4x10 Opening Setup Generator & Fortress Architect

Algorithmic reference and tactical generator for competitive 4x10 board configurations in Stratego, including Corner Flag fortresses, Bluff Defenses, Shoreline Traps, and Aggressive Spearheads.

🔗 **Interactive 4x10 Setups & Board Editor**: [4x10 Setups](https://strategocheatsheets.com/setups)  
🔗 **Combat Rules & Battle Judge**: [how to play stratego](https://strategocheatsheets.com/rules)  
🔗 **Complete Piece Rank & Dossier**: [Stratego Tactical Companion](https://strategocheatsheets.com/pieces)

---

## 🛡️ Archetypes of Stratego Formations

A standard Stratego army contains exactly 40 pieces deployed across four rows of 10 squares ($4 \times 10 = 40$).

### 1. The Corner Fortress (Defensive Standard)
- **Flag Position**: Square (1, 1) or (1, 10) in the back row.
- **Bomb Enclosure**: 3 Bombs triangularly encasing the Flag.
- **Miner Decoy**: Front row placement of Miners to bait early aggressive attacks.
- **Marshal Counter**: Marshal positioned on row 2, ready to strike enemy infiltrators that break the defensive perimeter.

### 2. The Center Bluff (Psychological Deployment)
- **Flag Position**: Square (1, 5) or (1, 6) in the back row, surrounded by high-ranking Officers rather than Bombs.
- **Bomb Screen**: Bombs deployed along row 3 to protect Scouts and Captains, creating a false fortress in one of the corners.

### 3. Shoreline Control (Aggressive Chokepoint)
- **Scout Probing**: Scouts deployed adjacent to the two central 2x2 lakes (columns 3-4 and 7-8) for turn-1 reconnaissance.
- **Lieutenant Support**: Fast response units positioned behind lake chokepoints to punish overextended enemy Scouts.

---

## 📐 Algorithmic Validation Matrix (JavaScript)

```javascript
/**
 * Validates a 4x10 Stratego setup for tournament legality.
 * @param {Array<Array<Object>>} board - 4 rows x 10 columns grid.
 * @returns {Object} validation status and counts.
 */
function validateStrategoSetup(board) {
  const PIECE_LIMITS = {
    Flag: 1,
    Bomb: 6,
    Spy: 1,
    Scout: 8,
    Miner: 5,
    Sergeant: 4,
    Lieutenant: 4,
    Captain: 4,
    Major: 3,
    Colonel: 2,
    General: 1,
    Marshal: 1
  };

  const counts = {};
  for (let r = 0; r < 4; r++) {
    for (let c = 0; c < 10; c++) {
      const piece = board[r][c];
      if (!piece) return { valid: false, error: `Empty square at (${r}, ${c})` };
      counts[piece.type] = (counts[piece.type] || 0) + 1;
    }
  }

  for (const [type, max] of Object.entries(PIECE_LIMITS)) {
    if ((counts[type] || 0) !== max) {
      return { valid: false, error: `Invalid count for ${type}: expected ${max}, found ${counts[type] || 0}` };
    }
  }

  return { valid: true, totalPieces: 40 };
}
```

For interactive drag-and-drop board setup, visual rank conversions, and printable strategy charts, explore the [Stratego Tactical Companion](https://strategocheatsheets.com/).
