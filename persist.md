# PERSIST

Re-apply roles or nicknames for users when they rejoin the server.

**Mute roles are re-applied automatically, this plugin is not required for that.**

`persist_nicknames` Enabling this re-applies any nickname user had prior to leaving server

`persist_voice_mutes` Enabling this re-applies any voice mutes user had before leaving

#### PLUGIN CODE

```yaml
  persist:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      persisted_roles:
        #Member role
        - "851852521206710273"
      persist_nicknames: true
      persist_voice_mutes: true
```
