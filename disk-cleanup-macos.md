# Disk cleanup (macOS)

## Overall disk usage

```bash
df -h
```

## Top-level home directory breakdown

```bash
du -sh ~/_/ ~/._/ 2>/dev/null | sort -rh | head -20
```

## Drill into Library

```bash
du -sh ~/Library/\*/ 2>/dev/null | sort -rh | head -15
```

## Drill into specific Library subfolders

```bash
du -sh ~/Library/Group\ Containers/_/ 2>/dev/null | sort -rh | head -10
du -sh ~/Library/Caches/_/ 2>/dev/null | sort -rh | head -10
du -sh ~/Library/Developer/_/ 2>/dev/null | sort -rh | head -10
du -sh ~/Library/Containers/_/ 2>/dev/null | sort -rh | head -10
```

## Find large files in Downloads

```bash
find ~/Downloads -type f -size +500M -exec ls -lh {} \; | sort -k5 -rh
```

## List folders in Downloads by size

```bash
du -sh ~/Downloads/\*/ 2>/dev/null | sort -rh
```

## Docker space usage

```bash
docker system df
docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.Size}}\t{{.CreatedSince}}" | sort -k3 -rh
```

## Find Python virtual environments

```bash
find ~ -type d \( -name ".venv" -o -name "venv" -o -name "env" \) -maxdepth 5 2>/dev/null -exec du -sh {} \; | sort -rh
```

## Conda envs

```bash
du -sh ~/miniconda3/envs/_ ~/anaconda3/envs/_ 2>/dev/null | sort -rh
```

## Node modules

```bash
find ~ -name "node_modules" -type d -maxdepth 5 2>/dev/null -exec du -sh {} \; | sort -rh | head -10
```
