## shell-script

- `AIRFLOW_PROJ_DIR` 변수로 정의된 값이 있으면 그 값을 출력하고, 없으면 `.`을 출력

```bash
echo ${AIRFLOW_PROJ_DIR:-.}
.
```
