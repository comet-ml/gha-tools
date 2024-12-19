# Update GitHub variable

Usage:
```
- name: Update Patch Version
      uses: comet-ml/gha-tools/update-gha-variable@main
      with:
        type_var_sec: repository
        name: "PATCH_VERSION"
        value: ${{ steps.set-values.outputs.patch }}
        environment: development
        app_id: ${{ secrets.APP_ID }}
        app_private_key: ${{ secrets.APP_PRIVATE_KEY }}
```
