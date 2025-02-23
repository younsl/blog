# Configuration

## Summary

This document describes the details of the configuration of the `void` theme.

## Configuration details

### Show more contents in main page

If you want to setup read more feature in main page, you need to set the following configuration in your `hugo.yaml` file.

```yaml
# <YOUR_HUGO_REPOSITORY>/hugo.yaml
params:
  entries:
  - post_list:
      limit: 5
      show_more: true
      show_more_text: ""
      # If all contents are located in the content/blog directory,
      # you can set show_more_url as "/blog"
      show_more_url: "/blog"
```

### Appearance

This theme supports three types of appearance: **dark mode**, **light mode**, and **auto**.

If you want to toggle **dark mode**, you need to set the following configuration in your `hugo.yaml` file.

```yaml
# <YOUR_HUGO_REPOSITORY>/hugo.yaml
params:
  theme_config:
    appearance: dark
```

If you want to toggle **light mode**, you need to set the following configuration in your `hugo.yaml` file.

```yaml
# <YOUR_HUGO_REPOSITORY>/hugo.yaml
params:
  theme_config:
    appearance: light
```

If you want to  automatically by user preference, you need to set the following configuration in your `hugo.yaml` file.

```yaml
# <YOUR_HUGO_REPOSITORY>/hugo.yaml
params:
  theme_config:
    appearance: auto
```

### Toggle footer

If you want to toggle footer appearance, you need to set the following configuration in your `hugo.yaml` file.

```yaml
# <YOUR_HUGO_REPOSITORY>/hugo.yaml
params:
  theme_config:
    isShowFooter: false
```

If you want to show footer, you need to set the following configuration in your `hugo.yaml` file.

```yaml
# <YOUR_HUGO_REPOSITORY>/hugo.yaml
params:
  theme_config:
    isShowFooter: true
```