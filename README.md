# DAO Governance Smart Contract

A comprehensive decentralized autonomous organization (DAO) governance system built with Clarity for the Stacks blockchain.

## Overview

This smart contract implements a full-featured DAO governance system with:

- Proposal creation and voting
- Treasury management
- Delegation system
- Emergency controls
- Return pool distribution
- Configurable governance parameters

## Core Features

### 1. Proposal System

- Create proposals with titles and descriptions
- Configurable voting periods
- Minimum and maximum proposal amounts
- Proposal fee system
- Quorum and super-majority requirements

### 2. Voting Mechanism

- One token, one vote system
- Vote delegation capabilities
- Time-locked voting periods
- Quorum tracking

### 3. Treasury Management

- Secure fund management
- Return pool distribution
- Claim system for returns
- Balance tracking

### 4. Security Features

- Emergency admin system
- Parameter validation
- Access controls
- Safety checks

## Contract Parameters

### Governance Parameters

```clarity
{
    proposal-fee: u100000,        // 0.1 STX
    min-proposal-amount: u1000000, // 1 STX
    max-proposal-amount: u1000000000, // 1000 STX
    voting-delay: u100,           // Blocks before voting starts
    voting-period: u144,          // ~1 day in blocks
    timelock-period: u72,         // ~12 hours in blocks
    quorum-threshold: u500,       // 50% in basis points
    super-majority: u667          // 66.7% in basis points
}
```

## Public Functions

### Proposal Management

#### `create-proposal`

Creates a new governance proposal.

```clarity
(create-proposal
    (title (string-ascii 100))
    (description (string-utf8 1000))
    (amount uint)
    (target principal))
```

#### `delegate-votes`

Delegates voting power to another member.

```clarity
(delegate-votes
    (delegate-to principal)
    (amount uint)
    (expiry uint))
```

### Return Pool Management

#### `create-return-pool`

Creates a return pool for proposal distributions.

```clarity
(create-return-pool
    (proposal-id uint)
    (total-amount uint))
```

#### `claim-returns`

Claims returns from a return pool.

```clarity
(claim-returns
    (proposal-id uint))
```

### Emergency Controls

#### `set-emergency-state`

Sets the emergency state of the DAO.

```clarity
(set-emergency-state
    (state bool))
```

#### `add-emergency-admin`

Adds an emergency administrator.

```clarity
(add-emergency-admin
    (admin principal))
```

## Read-Only Functions

### `get-member-info`

Retrieves member information.

```clarity
(get-member-info
    (member principal))
```

### `get-proposal-by-id`

Retrieves proposal details.

```clarity
(get-proposal-by-id
    (proposal-id uint))
```

### `get-dao-parameters`

Retrieves current DAO parameters.

```clarity
(get-dao-parameters)
```

## Error Codes

| Code | Description         |
| ---- | ------------------- |
| u100 | Not authorized      |
| u101 | Already voted       |
| u102 | Proposal expired    |
| u103 | Insufficient funds  |
| u104 | Invalid amount      |
| u105 | Proposal not active |
| u106 | Quorum not reached  |
| u110 | No delegate         |
| u111 | Invalid delegate    |
| u112 | Emergency active    |
| u113 | Not emergency       |
| u114 | Invalid parameter   |
| u115 | No returns          |

## Security Considerations

1. **Access Control**

   - Admin-only functions are protected
   - Emergency controls require proper authorization
   - Delegation system validates all parties

2. **Fund Safety**

   - Treasury balance checks
   - Return pool distribution validation
   - Claim verification

3. **Parameter Validation**
   - Amount boundaries
   - Timelock periods
   - Quorum thresholds

## Best Practices

1. **Proposal Creation**

   - Use descriptive titles
   - Provide detailed descriptions
   - Set appropriate amounts
   - Consider voting periods

2. **Voting**

   - Review proposal details carefully
   - Check delegation expiry
   - Verify voting power

3. **Return Pools**
   - Monitor distribution periods
   - Track claim status
   - Verify share calculations

## Development and Testing

1. Clone the repository
2. Deploy using Clarinet
3. Run the test suite
4. Use the console for interaction
