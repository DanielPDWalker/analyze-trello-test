# analyze-trello-test

Meltano project [file bundle](https://meltano.com/docs/command-line-interface.html#file-bundle) of Matatika datasets for `tap-trello`. These datasets are automatically added to your Matatika workspace when you initialize a `tap-trello` pipeline.

Files:
- [`analyze/datasets`](./bundle/analyze/datasets) (directory)

### Adding this file bundle to your own Meltano project

Add plugin to `discovery.yml`:
```yaml
files:
- name: analyze-trello-test
  namespace: tap_trello
  repo: https://github.com/DanielPDWalker/analyze-trello-test
  pip_url: git+https://github.com/DanielPDWalker/analyze-trello.git
```

Add plugin to your Meltano project:
```bash
# Add only the file bundle
meltano add files analyze-trello-test

# Add the file bundle as a related plugin through adding the Trello extractor
meltano add extractor --include-related tap-trello
```

### Adding this along with tap-trello as a custom plug-in for in Matatika

Go to data imports, click on `Custom Data Source` and copy and paste in:

```yaml
extractors:
  - name: tap-trello
    namespace: tap_trello
    pip_url: git+https://github.com/Matatika/tap-trello.git
    capabilities:
      - state
      - discover
      - catalog
    settings:
      - name: developer_api_key
        kind: password
      - name: access_token
        kind: password
      - name: start_date
files:
  - name: analyze-trello-test
    namespace: tap_trello
    update:
      analyze/datasets/tap-trello: true
    pip_url: git+https://github.com/DanielPDWalker/analyze-trello.git
```