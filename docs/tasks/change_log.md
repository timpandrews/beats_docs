# Change Log ![Change Log](../assets/icons/change_log.png){: width="4%"}  

```yaml title="change_log.yaml"
- version: "0.1.0-alpha"
  change_log_date: "2024-02-08"
  description: "Overview of the entire change_log/version."
  internal: False   
  live: True        
  working: False 
  entries:
  - type: "New Feature"
    title: "Initial implementation of Change Log"
    internal: False 
    description: "Detailed description of this entry."
  - type: "Enhancement"
    description: "Made Miscellaneous Formatting Changes"
    internal: False
    description: "Detailed description of this entry."
```
### ChangeLog - Fields
- version (text): <small>Version must be in 'MAJOR.MINOR.PATCH' or 'MAJOR.MINOR.PATCH-PRERELEASE' format."</small>
- change_log_date (text): <small>YYYY-MM-DD</small>
- description (text): <small>Overview of the entire change_log/version. This is not displayed in the change log and is only used for reference here.</small>  
- internal (boolean): <small>if internal only displayed for superusers</small>
- live (boolean): <small>if live, display in the change log</small>
- working (boolean): <small>if working, this is the latest change_log and is not completed and should not be diplayed in the change log</small>
- entries (list): <small>a list of all Change_log_detail items for this change log</small>

### ChangeLogDetail - Fields
- type (text):  <small>Acceptable values include: New Feature, Enhancement, Removed Feature, Bug Fix, Security</small>
- title (text):  <small>Text displayed in change log</small>
- internal (boolean): <small>if internal only display for superusers</small>
- description (text): <small>Detailed description of this entry.  This is NOT displayed in the change log and is only used for reference here

### To update the Change Log
#### Update Change Log as your working
- Keep a change log for the current/working change log.
- Add entries for new features, enhancements, etc.
#### Update Change Log when ready to push to Production
- As part of the final steps of preparing code for production (ie Testing & Linting)
- Update Change Log for to be included in push to production

##### Citations
<a href="https://semver.org/" target="_blank">semver.org</a> |
<a href="https://keepachangelog.com/en/1.1.0/" target="_blank">keepachangelog.com</a>
