# Interactive Widgets
## ipywidgets

 - Purpose: Build interactive widgets in Jupyter notebooks.

 - Typical Use Cases: Create sliders, buttons, dropdowns, interactive data visualization.

 - Basic Usage:
    ```python
    import ipywidgets as widgets
    from IPython.display import display

    slider = widgets.IntSlider(value=5, min=0, max=10, step=1, description="Value:")
    display(slider)
    ```

 - Interactive function binding:
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    from ipywidgets import interact

    def plot_func(freq):
        x = np.linspace(0, 2*np.pi, 100)
        y = np.sin(freq * x)
        plt.plot(x, y)
        plt.show()

    interact(plot_func, freq=(1, 10, 1))
    ```