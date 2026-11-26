# BitBadges Asset Registry

A TypeScript-based asset registry for the BitBadges Cosmos SDK chain, following the Osmosis Zone List format.

## Features

✅ **TypeScript Support** - Full type safety and IntelliSense  
✅ **JSON Schema Validation** - Comprehensive validation against the schema  
✅ **Custom Validation Rules** - Additional checks beyond JSON schema  
✅ **Testing Framework** - Jest-based test suite  
✅ **Development Tools** - ESLint, Prettier, and TypeScript configuration  
✅ **Osmosis Zone Compatible** - Follows the exact format used by Osmosis Zone  

## Project Structure

```
bitbadges-asset-registry/
├── src/
│   ├── types.ts              # TypeScript type definitions
│   ├── validator.ts          # Asset registry validator class
│   ├── validate.ts           # CLI validation script
│   ├── index.ts              # Main entry point
│   └── __tests__/
│       └── validator.test.ts # Test suite
├── zone_assets.schema.json   # JSON Schema for validation
├── assets.json              # Asset registry data
├── package.json             # Node.js dependencies and scripts
├── tsconfig.json            # TypeScript configuration
├── jest.config.js           # Jest test configuration
├── .eslintrc.js             # ESLint configuration
├── .prettierrc              # Prettier configuration
└── README.md                # This file
```

## Installation

```bash
# Install dependencies
npm install

# Build the project
npm run build

# Run validation
npm run validate

# Run tests
npm test

# Lint code
npm run lint

# Format code
npm run format
```

## Usage

### Command Line Validation

```bash
# Validate the asset registry
npm run validate
```

### Programmatic Usage

```typescript
import { AssetRegistryValidator, AssetRegistry } from 'bitbadges-asset-registry';

// Create validator instance
const validator = new AssetRegistryValidator();

// Validate from file
const result = validator.validateFile('./assets.json');

// Validate from object
const registry: AssetRegistry = {
  $schema: './zone_assets.schema.json',
  chain_name: 'bitbadges',
  assets: [
    {
      chain_name: 'bitbadges',
      base_denom: 'abadge',
      categories: ['defi'],
      override_properties: {
        symbol: 'BADGE',
        name: 'BitBadges Token'
      }
    }
  ]
};

const validationResult = validator.validate(registry);

if (validationResult.isValid) {
  console.log('✅ Registry is valid!');
} else {
  console.log('❌ Validation errors:', validationResult.errors);
}
```

## Asset Registry Structure

The asset registry follows the Osmosis Zone List format and includes:

### Required Fields for Each Asset

- `chain_name` - The name of the chain as used in the Cosmos Chain Registry
- `base_denom` - The base denomination (e.g., "abadge" for BitBadges token)

### Optional Fields

- `path` - The IBC path for the asset
- `osmosis_verified` - Whether the asset has verified status on Osmosis Zone
- `osmosis_unstable` - Whether the asset can reliably be transferred to/from Osmosis
- `osmosis_disabled` - Whether deposit/withdraw functions are disabled
- `is_alloyed` - Whether the asset is an Alloyed Asset on Osmosis
- `osmosis_unlisted` - Whether the asset should be temporarily unlisted
- `osmosis_validated` - Whether the asset has been confirmed to work correctly
- `listing_date_time_utc` - When the asset was listed (ISO 8601 format)
- `categories` - Array of categories the asset belongs to
- `override_properties` - Properties that override Chain Registry defaults

### Categories Available

- `defi` - DeFi protocols
- `meme` - Meme tokens
- `liquid_staking` - Liquid staking tokens
- `sail_initiative` - Sail initiative tokens
- `bridges` - Bridge tokens
- `nft_protocol` - NFT protocol tokens
- `depin` - DePIN tokens
- `ai` - AI-related tokens
- `stablecoin` - Stablecoins
- `privacy` - Privacy-focused tokens
- `social` - Social tokens
- `oracles` - Oracle tokens
- `dweb` - Decentralized web tokens
- `rwa` - Real-world asset tokens
- `gaming` - Gaming tokens
- `built_on_osmosis` - Tokens built on Osmosis

## Customizing for Your Chain

### 1. Update Chain Name

Replace "bitbadges" with your actual chain name in both the schema reference and the `chain_name` field.

### 2. Add Your Native Token

Update the first asset entry with your chain's native token information:

```json
{
  "chain_name": "yourchain",
  "base_denom": "uyourtoken",
  "path": "transfer/channel-0/uyourtoken",
  "override_properties": {
    "symbol": "YOURTOKEN",
    "name": "Your Chain Token",
    "coingecko_id": "your-token-id"
  }
}
```

### 3. Add IBC Assets

For each IBC connection, add an asset entry with the correct:
- `chain_name` of the source chain
- `base_denom` of the asset
- `path` with the correct IBC channel information

### 4. Update Logo URIs

Replace the logo URIs with actual paths to your token images in the Cosmos Chain Registry format.

## Development

### Scripts

- `npm run build` - Compile TypeScript to JavaScript
- `npm run dev` - Watch mode for development
- `npm run validate` - Validate the asset registry
- `npm test` - Run the test suite
- `npm run lint` - Lint the code
- `npm run format` - Format the code
- `npm run clean` - Clean build artifacts

### Adding New Assets

When adding new assets:

1. Ensure all required fields are present
2. Use the correct base denominations (e.g., "uatom" not "atom")
3. Verify IBC paths are correct
4. Add appropriate categories
5. Include proper logo URIs
6. Run validation: `npm run validate`
7. Run tests: `npm test`

## Integration with Osmosis Zone

This asset registry format is compatible with Osmosis Zone and can be used to:

1. List your assets on Osmosis Zone
2. Enable IBC transfers between your chain and Osmosis
3. Provide asset metadata for wallets and explorers
4. Enable trading pairs on Osmosis DEX

## Resources

- [Cosmos Chain Registry](https://github.com/cosmos/chain-registry)
- [Osmosis Zone](https://app.osmosis.zone/)
- [IBC Documentation](https://ibc.cosmos.network/)
- [JSON Schema Specification](https://json-schema.org/)
- [TypeScript Documentation](https://www.typescriptlang.org/) 