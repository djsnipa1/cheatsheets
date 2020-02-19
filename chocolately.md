# Chocolately Notes

## Listing Updated Applications

**Note**: You likely need to do the following commands in an administrative cmd/powershell prompt.

If you have version 0.9.8.33 or below installed:

```
choco version all
```

If you have 0.9.9+ installed:

```
choco upgrade all --noop
```

If you have choco 0.9.9.6+, you can use the `outdated` command.

```
choco outdated
```

Following that, if you actually want to upgrade \- in both versions you can follow with:

```
cup all -y
```

**Note:** `-y` will only work with 0.9.8.33+.

---
