# Dan Wallace's Ansible Collections

An index of my Ansible content. The roles that used to live here as individual
GitHub repositories (`ansible_common`, `ansible_docker_traefik`, …) have been
reorganized into **versioned collections** under the `danmwallace.*` namespace.
Each collection is its own repository and Galaxy release; this page just points to
them.

> If you followed an old `danmwallace/ansible_<role>` link, the role now lives
> inside one of the collections below and is addressed by its FQCN, e.g.
> `ansible_docker_traefik` → `danmwallace.docker.traefik`.

## Collections

| Collection | Version | Distribution | Roles |
| --- | --- | --- | --- |
| [`danmwallace.docker`](https://github.com/danmwallace/ansible-collection-docker) | 1.1.2 | Galaxy | `common`, `docker`, `traefik`, `adguard`, `arcane`, `baserow`, `grafana`, `it_tools`, `librechat`, `n8n`, `semaphore`, `unifi` |
| [`danmwallace.linux`](https://github.com/danmwallace/ansible-collection-linux) | 1.1.0 | Galaxy | `cloudflare_ssl`, `cockpit`, `restic_restore`, `raspberry_pi_network_toolkit` |
| [`danmwallace.fedora`](https://github.com/danmwallace/ansible-collection-fedora) | 1.0.1 | Galaxy | `hyprland` |
| [`danmwallace.azure`](https://github.com/danmwallace/ansible-collection-azure) | 1.0.1 | Galaxy | `azure_arc` |
| [`danmwallace.private`](https://github.com/danmwallace/ansible-collection-private) | 1.0.2 | GitHub only | `portfolio`, `vday`, `wsb` |
| [`danmwallace.ubuntu`](https://github.com/danmwallace/ansible-collection-ubuntu) | 1.0.0 | GitHub only | _none yet_ |

Roles are addressed by FQCN — `danmwallace.<collection>.<role>` (for example
`danmwallace.linux.cockpit` or `danmwallace.docker.adguard`).

### What each collection is for

- **`danmwallace.docker`** — roles for useful Docker containers in the homelab,
  most attaching to a shared Traefik `proxy_network` for SSL termination.
- **`danmwallace.linux`** — cross-distro Linux host configuration: SSL via
  Cloudflare DNS, Cockpit, Restic restore, the Raspberry Pi network toolkit.
- **`danmwallace.fedora`** — Fedora workstation / atomic-variant configuration
  (Hyprland, etc.).
- **`danmwallace.azure`** — Azure Arc and related cloud-native integrations.
- **`danmwallace.private`** — personal/private homelab roles (not published to
  Galaxy).
- **`danmwallace.ubuntu`** — Ubuntu-specific configuration; publishing is deferred
  until it carries roles.

## Using these collections

For the Galaxy-published collections, install directly:

```bash
ansible-galaxy collection install danmwallace.docker
```

To pin everything in a project, use a `requirements.yml`. The Galaxy collections
pin by version; the GitHub-only ones (`private`, `ubuntu`) install from their git
source:

```yaml
collections:
  - name: danmwallace.docker
    version: ">=1.1.2"
  - name: danmwallace.linux
    version: ">=1.1.0"
  - name: danmwallace.fedora
    version: ">=1.0.1"
  - name: danmwallace.azure
    version: ">=1.0.1"
  - name: https://github.com/danmwallace/ansible-collection-private.git
    type: git
    version: main
```

Then install with:

```bash
ansible-galaxy collection install -r requirements.yml
```

Reference a role from a collection by its FQCN in a play:

```yaml
- hosts: web
  become: true
  roles:
    - danmwallace.docker.traefik
    - danmwallace.docker.adguard
```

## License

Each collection is MIT licensed; see its repository for the authoritative
`galaxy.yml` and `LICENSE`.
