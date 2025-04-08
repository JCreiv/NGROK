
# NGROK

# **Step 1: Instalar ngrok**


Para instalar ngrok en **Debian Linux**, ejecuta el siguiente comando en tu terminal:

```bash
curl -sSL https://ngrok-agent.s3.amazonaws.com/ngrok.asc \
  | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null \
  && echo "deb https://ngrok-agent.s3.amazonaws.com buster main" \
  | sudo tee /etc/apt/sources.list.d/ngrok.list \
  && sudo apt update \
  && sudo apt install ngrok
```


---

El agente ngrok es un programa CLI sin dependencias que funciona en todos los sistemas operativos principales. Para verificar que lo instalaste correctamente, ejecuta el siguiente comando en tu terminal:

```bash
ngrok
```

Esto debería mostrar el texto de ayuda de ngrok si la instalación fue exitosa.

---

# **Step 2: Conectar tu cuenta

A continuación, conecta tu agente ngrok a tu cuenta ngrok. Si aún no tienes una cuenta, regístrate en ngrok. Copia tu **ngrok authtoken** desde el panel de control de ngrok.

Ejecuta el siguiente comando en tu terminal para instalar el **authtoken** y conectar el agente ngrok a tu cuenta.

```bash
ngrok config add-authtoken <TOKEN>
```

Reemplaza `<TOKEN>` con el token de autenticación que obtuviste desde tu panel de control.

---

# **Step 3: Exponer servicio http**

Inicia ngrok ejecutando el siguiente comando.

```bash
ngrok http http://localhost:8000
```

Asumimos que tienes una aplicación web funcionando en `http://localhost:8080`. Si tu aplicación está escuchando en una URL diferente, ajusta el comando anterior para que coincida con la dirección correcta.

### POC:

![](ANEXOS/Pasted%20image%2020250406230120.png)



# **Step 4: Usar el mismo dominio

Si deseas mantener la misma URL cada vez que uses ngrok, crea un dominio estático en tu panel de control y luego usa la opción `--url` para indicarle al agente ngrok que lo utilice.

```bash
ngrok http 8000 --url https://<dominio_generado>
```

### POC:


![](ANEXOS/Pasted%20image%2020250407022000.png)


![](ANEXOS/Pasted%20image%2020250407022122.png)



# **Step 5: Securizar tu app

Es posible que no quieras que todos puedan acceder a tu aplicación. ngrok puede agregar rápidamente autenticación a tu aplicación sin necesidad de realizar cambios. Si tu cuenta de Google es [email@example.com](mailto:alan@example.com), puedes restringir el acceso solo para ti mismo ejecutando ngrok con:

```bash
ngrok http http://localhost:8000 --oauth google --oauth-allow-email email@example.com
```

Cualquier persona que intente acceder a tu aplicación será invitada a iniciar sesión con Google, y solo tu cuenta podrá acceder. Ten en cuenta que cuando reinicies ngrok, si no especificas la opción `--url`, la URL de tu aplicación cambiará, así que asegúrate de visitar la nueva URL.

# **Opciones de autenticación ngrok **

ngrok admite muchos tipos de autenticación, incluyendo:

- **OAuth** (lo que acabamos de usar)
    
- **Autenticación básica** 
    
- **Restricciones por IP**
    
- **Validación JWT**

Etc.
### POC:


![](ANEXOS/Pasted%20image%2020250407022540.png)

![](ANEXOS/Pasted%20image%2020250407024025.png)

