# Metrics & Result Saving

## Evaluation Framework
 - Key Components to be record
   - dataset name
   - model name
   - args setting
 - Saving Method
   - directory based (for logs)
     - ```./dataset_name/model_name/args_setting.json```
     - every time different file
       - python code template
        ```python
        def get_next_filename(
            self,
            chain_params: SupplyChainParams,
            save_type: str,
            multi_turn: bool = False,
            extension: str = "csv",
        ) -> pathlib.Path:
          """auto generate the path to save evaluation results"""

          index = 0
          while True:
              # 构建文件名，包含索引
              path = self.get_filename(
                  chain_params=chain_params,
                  save_type=save_type,
                  index=index,
                  extension=extension,
              )

              # 如果文件不存在，则返回该路径
              if not path.exists():
                  return path

              index += 1
        ```
   - dataframe based (for metrics)
     - columns including dataset_name, model_naem, etc.
     - all in one file