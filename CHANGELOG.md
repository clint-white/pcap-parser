# Change Log

## [Unreleased][unreleased]

### Added

### Changed/Fixed

## 0.14.0

### Changed/Fixed

- Properly handle errors when decoding timestamp resolution (#16)
- Remove deprecated pcapng parsing functions

## 0.13.3

### Changed/Fixed

- Fix computation of resolution for pcapng, when using power of two (#16)

## 0.13.2

### Changed/Fixed

- Add explicit configuration flags for rustdoc (#17)

## 0.13.1

### Changed/Fixed

- PcapReaderIterator: add method to test if reader is exhausted
  This also fix a case where reader returned Incomplete because it could
  not distinguish EOF and a request of 0 bytes.

## 0.13.0

### Changed/Fixed

- Upgrade to nom 7
- Set MSRV to 1.46

## 0.12.0

### Added

- Add method to get total number of consumed bytes for PcapReaderIterator

### Changed/Fixed

- Report error instead of EOF when a block is incomplete and no more data is available
- Add input to error type (helps diagnosing errors)
  `PcapError` now usually has a lifetime

## 0.11.1

### Changed/Fixed

- Fix potential integer overflows when aligning data in EPB and BSD
  Overflow was harmless, length arguments is tested after aligning anyway
- pcapng: use streaming parsers, return incomplete instead of eof (#13)

## 0.11.0

### Added

- Add trait PcapNGPacketBlock

### Changed/Fixed

- Rewrite Pcap and PcapNG block parsing functions
  - the 'block_type' field is always read as little-endian
    This is used to get the endianness for the encoding of the block.
  - new parsing functions are faster
- Use consistent names for big-endian/little-endian versions:
  - 'parse_block' is deprecated and replaced by 'parse_block_le'
  - 'parse_enhancedpacketblock' is deprecated and replaced by 'parse_enhancedpacketblock_le'
  - same for all parsing functions with '_le'
  - 'parse_sectionheader' is replaced by 'parse_sectionheaderblock'
- Functions that parse a specific block type (for ex. EPB) return the matching type
  (EnhancedPacketBlock) with encapsulating it in a Block
- Improve documentation and examples

## 0.10.1

### Changed/Fixed

- Re-export nom so crate users do not need to import it
- Convert doc links to short form when possible

## 0.10.0

### Changed/Fixed

- Upgrade to nom 6

## 0.9.4

### Added

- Add trait PartialEq to PcapError

### Changed/Fixed

- Improve error handling in create_reader (if input is empty or incomplete)
- Set MSRV to 1.44
- Update consume() documentation, it does not refill buffer (Closes #9)

## 0.9.3

### Added

- Add support for nanosecond-resolution legacy PCAP files

## 0.9.2

### Added

- Add Error trait to PcapError
- Edition 2018: remove all "extern crate" statements
- QA: warn if using unstable features, forbid unsafe code

## 0.9.1

### Added

- Check magic constants when reading DSB and SJE blocks
- Add `ToVec` implementation for SJE, DCB and Block

## 0.9.0

### Added

- Add `Default` trait to `Linktype`
- Add `NameRecordType` constants
- pcap-ng: add method to get the (normalized) magic of blocks
- Add support for Decryption Secrets Block (DSB)
- Add support for Systemd Journal Export Block (SJE)

### Changed/Fixed

- Improve documentation (remove relative links, broken outside docs.rs)

## 0.8.4

- Add method to access data of the PcapReaderIterator buffer
- Fix all clippy warnings

## 0.8.3

- Avoid integer overflow in `parse_name_record` edge case

## 0.8.2

- Remove byteorder crate, use functions from std
- Return Eof if refill failed (avoid infinite loop)

## 0.8.1

- Upgrade to cookie-factory 0.3.0

## 0.8.0

- Add basic support for serialization (little-endian only)
- Add basic support for Wireshark exported PDUs
- Add traits Clone and Debug to PacketData
- Move data parsing functions to a subdirectory

## 0.7.1

- Fix wrong EOF detection
- Fix handling of incomplete reads (in example)

## 0.7.0

- Upgrade to nom 5
  - Breaking API changes, mainly for error types

## 0.6.1

- Make LegacyPcapBlock a regular structure with parser, and add serialization

## 0.6.0

- Complete rewrite of the crate (breaks API)
- Add streaming parser iterators
- Replace Packet with Blocks
  - Allows handling of non-data blocks
  - Handles correctly timestamps and resolution
  - Remove incorrect or deprecated code
- Better parsing of all variants (BE/LE, block types, etc.)
- Better (and panic-free) functions to extract block contents
- Set edition to 2018
- Better documentation

## 0.5.1

- Fix computation of timestamp for high-resolution pcap-ng

