# Interactive Widgets

## ipywidgets

- Purpose: build interactive controls in Jupyter notebooks (sliders, dropdowns, buttons)
- Install: `pip install ipywidgets`

### Quick Usage

```python
import ipywidgets as widgets
from IPython.display import display

slider = widgets.IntSlider(value=5, min=0, max=10, step=1, description="Value:")
display(slider)
```

### Bind to a Function with `interact`

```python
from ipywidgets import interact
import matplotlib.pyplot as plt
import numpy as np

def plot_func(freq):
    x = np.linspace(0, 2 * np.pi, 100)
    plt.plot(x, np.sin(freq * x))
    plt.show()

interact(plot_func, freq=(1, 10, 1))  # auto-generates a slider
```

### Common Widget Types

| Widget | Use Case |
|--------|----------|
| `IntSlider`, `FloatSlider` | numeric parameter sweep |
| `Dropdown` | choose from a list of options |
| `Checkbox` | toggle boolean flags |
| `Text`, `Textarea` | text input |
| `Output` | capture and display output in a controlled area |

### Tips

- Use `interact_manual` to add a "Run" button instead of auto-updating on every change (good for slow functions)
- Use `widgets.Output()` to display plots/outputs without them jumping around
- Combine with `HBox` / `VBox` for custom layouts:
  ```python
  widgets.HBox([slider, widgets.Label("← drag me")])
  ```
