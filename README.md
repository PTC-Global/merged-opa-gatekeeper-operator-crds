This is a temporary workaround for having all opa gatekeeper-operator CRDs in a single file:

Follow these steps to get the file ready.

```bash
OPA_GATEKEEPER_OPERATOR_VERSION= # e.g. v3.5.1
NEW_MERGED_CRD_FILE=opa-gatekeeper-operator-crds-${OPA_GATEKEEPER_OPERATOR_VERSION:?}.yaml
test -d gatekeeper || git clone https://github.com/open-policy-agent/gatekeeper
pushd ./gatekeeper; git pull -a; git checkout ${OPA_GATEKEEPER_OPERATOR_VERSION:?}; popd
for file in ./gatekeeper/charts/gatekeeper/crds/*.yaml; do
    echo "---" >> ${NEW_MERGED_CRD_FILE:?}
    cat $file >> ${NEW_MERGED_CRD_FILE:?}
done
git add ${NEW_MERGED_CRD_FILE:?}
git commit -m "Added opa gatekeeper operator CRDs file for ${OPA_GATEKEEPER_OPERATOR_VERSION:?}"
git push
```
