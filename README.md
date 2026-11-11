# LynqTerm

LynqTerm is a native Android terminal app built with Kotlin and Jetpack Compose. It provides a lightweight command interface for file management, launching installed apps, and basic network diagnostics.

- Android 10 (API 29) and newer
- No root access required
- Dark terminal interface with green output and a blue directory prompt
- Commands are implemented as independent classes and registered in one command registry

## Screenshot

_Add an application screenshot here after the first device build._

## Commands

| Command | Usage | Description |
|---|---|---|
| `pwd` | `pwd` | Print the current directory |
| `cd` | `cd [path]` | Change the current directory |
| `ls` | `ls [-l] [-a] [path]` | List files and directories |
| `cat` | `cat <file>` | Print a text file up to 200 KB |
| `mkdir` | `mkdir <name>` | Create a directory |
| `rm` | `rm [-r] [-y] <path>` | Remove files, dry-run by default |
| `apps` | `apps [filter]` | List launchable apps |
| `open` | `open <name or package>` | Launch an installed app |
| `ping` | `ping [-c N] <host>` | Send ICMP echo requests |
| `netinfo` | `netinfo` | Show network type, IP, DNS and gateway |
| `port` | `port <host> <port> [timeout_ms]` | Test one TCP port |
| `dns` | `dns <host>` | Resolve a hostname |
| `storage` | `storage [settings]` | Check or configure shared-storage access |
| `help` | `help` | List available commands |
| `man` | `man <command>` | Show a command manual |
| `clear` | `clear` | Clear terminal output |
| `history` | `history` | Show session command history |

## Install

1. Download the APK from the GitHub Releases page.
2. Allow installation from the browser or file manager when Android prompts you.
3. Install LynqTerm.
4. On first launch, grant the requested storage access if you want to manage shared files. On Android 11 and newer, LynqTerm opens the system All files access page. You can check access later with `storage`, or open the settings page with `storage settings`.

## Permissions

- `INTERNET`: required for DNS, ping and TCP connection tests.
- `ACCESS_NETWORK_STATE`: reads the active network and its properties.
- `ACCESS_WIFI_STATE`: supports network diagnostics. The app does not read the Wi-Fi SSID.
- `MANAGE_EXTERNAL_STORAGE`: enables broad shared-storage file management on Android 11 and newer. Android restricts `Android/data` and `Android/obb` even with this access.
- `READ_EXTERNAL_STORAGE` and `WRITE_EXTERNAL_STORAGE`: shared-storage access on Android 10. Android 11 and newer use the All files access setting instead.
- `QUERY_ALL_PACKAGES`: discovers installed launchable apps for `apps` and `open`.

LynqTerm is distributed through GitHub Releases, not Google Play. Google Play has additional restrictions on broad file access and installed-app visibility.

## Build

Requirements: JDK 17, Android SDK Platform 35, Android Build Tools, and Gradle 8.9.

```bash
gradle testDebugUnitTest assembleDebug
```

The project targets Android 10 (API 29) and newer. The minimum SDK is intentionally API 29, even though earlier Android versions can support adaptive icons.

The debug APK is generated at `app/build/outputs/apk/debug/app-debug.apk`.

## Release signing

Add these GitHub repository secrets before pushing a version tag:

- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

The release workflow decodes the keystore into the runner's temporary directory and builds a signed release APK. Never commit keystores, passwords, tokens or `local.properties`.

## Platform limitations

- Android 11 and newer restrict access to `Android/data` and `Android/obb`, even with All files access.
- Raw packet capture, ARP scanning, MAC discovery and unrestricted raw sockets require capabilities unavailable to ordinary non-rooted apps.
- Google Play restricts broad file access and installed-app visibility. LynqTerm is intended for direct distribution through GitHub Releases.

## Roadmap

- Traceroute using TTL stepping
- HTTP timing diagnostics
- Command aliases
- Terminal themes
- Session export
- Optional VPN-based traffic monitor

## Author

Jean Marie Nyajura, LynqIQ

- Portfolio: https://okalmary254.netlify.app
- LynqIQ: https://lynqiq.com

## License

MIT. See [LICENSE](LICENSE).
