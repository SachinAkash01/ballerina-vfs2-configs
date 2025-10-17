# VFS Configuration Analysis - Ballerina FTP Module

## Current VFS Configurations

### FTP Protocol

| Configuration | VFS Method | Description | User Configurable |
|--------------|------------|-------------|-------------------|
| `userDirIsRoot` | `setUserDirIsRoot(boolean)` | Treats the login home directory as the root (`/`) and prevents VFS from attempting to change to the actual server root | ✅ Yes |
| `passiveMode` | `setPassiveMode(boolean)` | Enables passive mode for FTP connections (useful for NAT/firewall scenarios) | ❌ No (internal only) |

### SFTP Protocol

| Configuration | VFS Method | Description | User Configurable |
|--------------|------------|-------------|-------------------|
| `userDirIsRoot` | `setUserDirIsRoot(boolean)` | Treats the login home directory as the root (`/`) and prevents VFS from attempting to change to the actual server root | ✅ Yes |
| `preferredAuthentications` | `setPreferredAuthentications(String)` | Specifies the order of authentication methods to try (e.g., "publickey,password") | ✅ Yes |
| `identityInfo` | `setIdentityInfo(IdentityInfo)` | Configures SSH private key file and passphrase for key-based authentication | ✅ Yes |
| `strictHostKeyChecking` | `setStrictHostKeyChecking(String)` | Controls host key verification ("yes", "no", "ask") | ✅ Yes (conditional) |
| `connectTimeout` | `setConnectTimeout(Duration)` | Timeout for establishing the initial SSH connection | ❌ No (hardcoded to 10 seconds) |

---

## Missing VFS Configurations

### FTP Protocol

| Configuration | VFS Method | Description |
|--------------|------------|-------------|
| `activePortRange` | `setActivePortRange(Range)` | Configures the range of ports to use for active mode data connections |
| `autodetectUtf8` | `setAutodetectUtf8(Boolean)` | Enables/disables automatic detection of UTF-8 encoding support on the server |
| `connectTimeout` | `setConnectTimeout(Duration)` | Timeout for establishing the initial FTP control connection |
| `connectTimeout` (deprecated) | `setConnectTimeout(Integer)` | Timeout in milliseconds for initial control connection (deprecated - use Duration variant) |
| `controlEncoding` | `setControlEncoding(Charset)` | Character encoding for FTP control commands and responses (e.g., UTF-8, ISO-8859-1) |
| `controlEncoding` (deprecated) | `setControlEncoding(String)` | Control channel encoding as string (deprecated - use Charset variant) |
| `controlKeepAliveReplyTimeout` | `setControlKeepAliveReplyTimeout(Duration)` | Timeout for waiting for keep-alive reply messages from the server |
| `controlKeepAliveTimeout` | `setControlKeepAliveTimeout(Duration)` | Timeout for sending keep-alive signals to maintain long-running control connections |
| `dataTimeout` | `setDataTimeout(Duration)` | Timeout for data channel operations (file transfers) |
| `dataTimeout` (deprecated) | `setDataTimeout(Integer)` | Timeout in milliseconds for data operations (deprecated - use Duration variant) |
| `defaultDateFormat` | `setDefaultDateFormat(String)` | Date format string for parsing file timestamps in FTP directory listings |
| `entryParser` | `setEntryParser(String)` | Fully qualified class name of a custom FTP directory listing parser for non-standard FTP servers |
| `entryParserFactory` | `setEntryParserFactory(FTPFileEntryParserFactory)` | Custom factory for creating FTP directory listing parsers |
| `fileType` | `setFileType(FtpFileType)` | Sets the file transfer type (ASCII, BINARY, etc.) |
| `mdtmLastModifiedTime` | `setMdtmLastModifiedTime(boolean)` | Enables/disables using the MDTM command to retrieve file modification times |
| `proxy` | `setProxy(Proxy)` | Configures HTTP/SOCKS proxy for FTP connections |
| `recentDateFormat` | `setRecentDateFormat(String)` | Date format string for parsing recent file timestamps (files modified within the current year) |
| `remoteVerification` | `setRemoteVerification(boolean)` | Enables or disables verification of the remote FTP server |
| `serverLanguageCode` | `setServerLanguageCode(String)` | Sets the language code for the FTP server (for parsing server messages) |
| `serverTimeZoneId` | `setServerTimeZoneId(String)` | Sets the time zone ID of the FTP server for correct timestamp interpretation |
| `shortMonthNames` | `setShortMonthNames(String[])` | Configures custom short month names for parsing FTP directory listings |
| `soTimeout` | `setSoTimeout(Duration)` | Timeout for socket read/write operations during FTP commands |
| `soTimeout` (deprecated) | `setSoTimeout(Integer)` | Socket timeout in milliseconds (deprecated - use Duration variant) |
| `transferAbortedOkReplyCodes` | `setTransferAbortedOkReplyCodes(List)` | Defines acceptable FTP reply codes when closing data streams to prevent errors on legitimate stream closures |

### SFTP Protocol

| Configuration | VFS Method | Description |
|--------------|------------|-------------|
| `compression` | `setCompression(String)` | Comma-separated list of compression algorithms to use (e.g., "zlib,none") |
| `configRepository` | `setConfigRepository(ConfigRepository)` | SSH configuration repository (e.g., OpenSSH config files) |
| `connectTimeoutMillis` (deprecated) | `setConnectTimeoutMillis(Integer)` | Connect timeout in milliseconds (deprecated - use setConnectTimeout with Duration) |
| `disableDetectExecChannel` | `setDisableDetectExecChannel(boolean)` | Controls whether exec channel detection is disabled |
| `fileNameEncoding` | `setFileNameEncoding(String)` | Character encoding for SFTP filenames (e.g., "UTF-8") |
| `identities` (deprecated) | `setIdentities(File...)` | Sets private key files for authentication (deprecated - use setIdentityProvider) |
| `identityInfo` (deprecated) | `setIdentityInfo(IdentityInfo...)` | Sets identity information objects (deprecated - use setIdentityProvider) |
| `identityProvider` | `setIdentityProvider(IdentityProvider...)` | Configures identity providers for SSH key-based authentication |
| `identityRepositoryFactory` | `setIdentityRepositoryFactory(IdentityRepositoryFactory)` | Factory for creating SSH identity repositories (enables SSH agent support) |
| `keyExchangeAlgorithm` | `setKeyExchangeAlgorithm(String)` | Specific key exchange algorithm to use for SSH connections |
| `knownHosts` | `setKnownHosts(File)` | Path to SSH known_hosts file for host key verification |
| `loadOpenSshConfig` | `setLoadOpenSSHConfig(boolean)` | Automatically load SSH configuration from OpenSSH config files (~/.ssh/config) |
| `proxyCommand` | `setProxyCommand(String)` | Command to execute on proxy host for stream proxy connections |
| `proxyHost` | `setProxyHost(String)` | Hostname or IP address of the proxy server for SFTP connections |
| `proxyOptions` | `setProxyOptions(FileSystemOptions)` | Connection options for the proxy host |
| `proxyPassword` | `setProxyPassword(String)` | Password for proxy authentication |
| `proxyPort` | `setProxyPort(int)` | Port number of the proxy server |
| `proxyType` | `setProxyType(SftpFileSystemConfigBuilder.ProxyType)` | Type of proxy to use (HTTP, SOCKS5, or STREAM) |
| `proxyUser` | `setProxyUser(String)` | Username for proxy authentication |
| `sessionTimeout` | `setSessionTimeout(Duration)` | Timeout for SSH session operations |
| `sessionTimeoutMillis` (deprecated) | `setSessionTimeoutMillis(Integer)` | Session timeout in milliseconds (deprecated - use setSessionTimeout with Duration) |
| `timeout` (deprecated) | `setTimeout(Integer)` | Session timeout in milliseconds (deprecated - use setSessionTimeout) |
| `userInfo` | `setUserInfo(UserInfo)` | Custom JSch UserInfo implementation for interactive authentication scenarios |

---

## Summary

### FTP Protocol
- **Currently Exposed:** 2 configurations (1 user-configurable, 1 internal only)
- **Missing:** 24 configurations (including deprecated variants)
  - 20 current/recommended methods
  - 4 deprecated methods

### SFTP Protocol
- **Currently Exposed:** 5 configurations (4 user-configurable, 1 hardcoded)
- **Missing:** 23 configurations (including deprecated variants)
  - 18 current/recommended methods
  - 5 deprecated methods

### Notes
- Deprecated methods are included for completeness but should generally be avoided in favor of their modern equivalents
- The deprecated methods typically use `Integer` (milliseconds) instead of `Duration` objects
- Methods like `setIdentities` and `setIdentityInfo` are deprecated in favor of `setIdentityProvider`

---

## References

- [FTP VFS Configuration Builder](https://commons.apache.org/proper/commons-vfs/commons-vfs2/apidocs/org/apache/commons/vfs2/provider/ftp/FtpFileSystemConfigBuilder.html)
- [SFTP VFS Configuration Builder](https://commons.apache.org/proper/commons-vfs/commons-vfs2/apidocs/org/apache/commons/vfs2/provider/sftp/SftpFileSystemConfigBuilder.html)
- Implementation: `native/src/main/java/io/ballerina/stdlib/ftp/transport/server/util/FileTransportUtils.java`
