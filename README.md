# PasarGuard:
SQLALCHEMY_DATABASE_URL

postgresql+asyncpg://${{Postgres.PGUSER}}:${{Postgres.PGPASSWORD}}@${{Postgres.PGHOST}}:${{Postgres.PGPORT}}/${{Postgres.PGDATABASE}}

# PasarGuard-Node:
/var/lib/pg-node   <= volume node
# New Create:
caddy:2-alpine <= add proxy
# Run Code In Proxy:
sh -c "{ echo ':8080 {'; echo \"  reverse_proxy https://$PANEL_UPSTREAM {\"; echo '    transport http {'; echo '      tls_insecure_skip_verify'; echo '    }'; echo '  }'; echo '}'; } > /etc/caddy/Caddyfile; exec caddy run --config /etc/caddy/Caddyfile --adapter caddyfile"      <start command

PANEL_UPSTREAM <= varible In Proxy

${{PasarGuard.RAILWAY_PRIVATE_DOMAIN}}:8000 <= varible panel



# Port:
PasarGuard-Node:
8880
Proxy:
8080
