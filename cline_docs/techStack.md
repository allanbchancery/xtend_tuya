# Tech Stack

## Core Technologies

### Home Assistant Integration Framework
- **Home Assistant Core**: Custom component architecture
- **Config Flow**: User interface for setup and configuration
- **Entity Framework**: Device and entity management
- **Device Registry**: Device identification and management

### Tuya SDK Dependencies
- **tuya_sharing**: Official Tuya sharing SDK for QR code authentication
- **tuya_iot**: Official Tuya IoT SDK for OpenAPI authentication
- **LoginControl**: QR code generation and authentication handling

### Authentication Methods

#### 1. QR Code Authentication (Primary)
- **Library**: `tuya_sharing.LoginControl`
- **Flow**: Generate QR code → User scans with mobile app → Token exchange
- **Client ID**: `HA_3y9q4ak7g4ephrvke`
- **Schema**: `haauthorize`

#### 2. OpenAPI Authentication (Secondary)
- **Library**: `tuya_iot.TuyaOpenAPI` (wrapped in `XTIOTOpenAPI`)
- **Requirements**: Access ID, Access Secret, Username, Password
- **Auth Types**: CUSTOM, SMART_HOME
- **App Types**: "", TUYA_SMART_APP, SMARTLIFE_APP

### Custom Components

#### Multi-Manager Architecture
- **MultiManager**: Central coordination of multiple authentication sources
- **XTSharingDeviceManager**: Handles tuya_sharing integration
- **XTIOTDeviceManager**: Handles tuya_iot integration
- **XTIOTOpenAPI**: Custom wrapper around TuyaOpenAPI with enhanced error handling

#### Device Management
- **XTDevice**: Extended device class with additional functionality
- **XTDeviceMap**: Device mapping with source priority
- **XTMergingManager**: Merges devices from multiple sources
- **MultiDeviceListener**: Handles device state updates

### Regional Endpoints
- **America**: `https://openapi.tuyaus.com`
- **Europe**: `https://openapi.tuyaeu.com`
- **China**: `https://openapi.tuyacn.com`
- **India**: `https://openapi.tuyain.com`
- **Singapore**: `https://openapi-sg.iotbing.com`

### Error Handling & Debugging
- **Issue Management**: Built-in issue reporting system
- **Device Watcher**: Debug message tracking
- **Retry Logic**: Automatic reconnection and token refresh
- **Logging**: Comprehensive logging with tuya_sharing suppression

## Architecture Decisions

### Why Multiple Authentication Methods?
- **Flexibility**: Support different user scenarios and preferences
- **Fallback**: If one method fails, users can try another
- **Feature Coverage**: Different methods provide different capabilities

### Why Custom OpenAPI Wrapper?
- **Enhanced Error Handling**: Better retry logic and error reporting
- **Token Management**: Automatic refresh and reconnection
- **Non-User API Support**: Support for device operations without user context

### Why Multi-Manager Pattern?
- **Source Aggregation**: Combine devices from multiple Tuya sources
- **Priority Management**: Handle conflicts between different data sources
- **Extensibility**: Easy to add new authentication sources
