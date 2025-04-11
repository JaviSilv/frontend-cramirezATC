<template>
  <div class="dashboard-container">
      <BarraLateralDashboard />
    <div class="main-content">
      <BarraSuperiorDashboard />
    <div class="container">

    <h2 class="tituloformulario">Formulario de Registro</h2>

    <div class="formulario-all">
      <form @submit.prevent="formularioClientevarios">
        <h3>Datos Personales</h3>

        <label>Apellido y Nombre:</label>
        <input v-model="form.nombreCliente" type="text"  @input="form.nombreCliente = form.nombreCliente.replace(/[0-9]/g, '')" />

        <label>Ocupación:</label>
        <input type="text" v-model="form.ocupacionCliente" placeholder="Ingrese su ocupación" @input="form.ocupacionCliente = form.ocupacionCliente.replace(/[0-9]/g, '')">

        <label for="tipoIdentificacion">Tipo de Identificación:</label>
        <select v-model="form.tipoIdentificacion" id="tipoIdentificacion">
          <option v-for="tipo in tipoIdentificacion" :key="tipo.id" :value="tipo.id">{{ tipo.nombre }}</option>
        </select>

        <label>Número de Identificación:</label>
        <input v-model="form.numIdentificacionUsuario" type="text" @input="form.numIdentificacionUsuario = form.numIdentificacionUsuario.replace(/[^0-9]/g, '')"  />

        <label for="paisOrigen">País de Origen:</label>
        <select v-model="form.paisOrigen" id="paisOrigen">
          <option disabled value="">Seleccione un país</option>
          <option v-for="pais in paises" :key="pais.id" :value="pais.id">{{ pais.nombre }}</option>
        </select>

        <label for="paisResidencia">País de Residencia:</label>
        <select v-model="form.paisdeResidencia" id="paisResidencia">
          <option disabled value="">Seleccione un país</option>
          <option v-for="residencia in residencias" :key="residencia.id" :value="residencia.id">{{ residencia.nombre }}</option>
        </select>

        <label for="departamento">Departamento:</label>
        <select v-model="form.departamento" id="departamento">
          <option value="" disabled>Selecciona un departamento</option>
          <option v-for="departamento in departamentos" :key="departamento.id" :value="departamento.id">{{ departamento.nombre }}</option>
        </select>

        <label>Provincia:</label>
        <select v-model="form.provincia">
          <option value="" disabled selected>Seleccione una provincia</option>
          <option v-for="provincia in provinciasFiltradas" :key="provincia.id" :value="provincia.id">{{ provincia.nombre }}</option>
        </select>

        <label>Distrito:</label>
        <select v-model="form.distrito">
          <option value="" disabled selected>Seleccione un distrito</option>
          <option v-for="distrito in distritosFiltrados" :key="distrito.id" :value="distrito.id">{{ distrito.nombre }}</option>
        </select>

        <label>Dirección:</label>
        <input v-model="form.direccion" type="text"  />

        <label>Correo Electrónico:</label>
        <div class="email-input">
          <input v-model="form.correoUsuario" type="email" placeholder="usuario@dominio.com"  />
        </div>

        <label for="prefijoTelefonico">Número Telefónico:</label>
        <div style="display: flex; gap: 5px;">
          <select v-model="form.prefijoTelefonico" id="prefijoTelefonico">
            <option v-for="prefijo in prefijos" :key="prefijo.id" :value="prefijo.id">{{ prefijo.codigo }}</option>
          </select>
          <input v-model="form.numTelefonico" type="text" id="numTelefonico" placeholder="Ingrese su número" @input="form.numTelefonico = form.numTelefonico.replace(/[^0-9]/g, '')" />
        </div>

        <label for="estadoCivil">Estado Civil:</label>
        <select v-model="form.estadoCivil" id="estadoCivil">
          <option v-for="estado in estadoCivil" :key="estado.id" :value="estado.id">{{ estado.nombre }}</option>
        </select>


        <div v-if="form.estadoCivil === 2">

          <h3 class="titulodatoslotes">Datos del Cónyuge</h3>

          <label>Nombre y Apellido:</label>
          <input v-model="form.conyuge.nombreClienteConyuge" type="text"  @input="form.conyuge.nombreClienteConyuge = form.conyuge.nombreClienteConyuge.replace(/[0-9]/g, '')"/>

          <label>Ocupación:</label>
          <input type="text" v-model="form.conyuge.ocupacionClienteConyuge" placeholder="Ingrese su ocupación" @input="form.conyuge.ocupacionClienteConyuge = form.conyuge.ocupacionClienteConyuge.replace(/[0-9]/g, '')">


          <label for="tipoIdentificacion">Tipo de Identificación:</label>
          <select v-model="form.conyuge.tipoIdentificacionClienteConyuge" id="tipoIdentificacion">
            <option v-for="tipo in tipoIdentificacion" :key="tipo.id" :value="tipo.id">{{ tipo.nombre }}</option>
          </select>

          <label>Número de Identificación:</label>
          <input v-model="form.conyuge.numIdentificacionClienteConyuge" type="text" @input="form.conyuge.numIdentificacionClienteConyuge = form.conyuge.numIdentificacionClienteConyuge.replace(/[^0-9]/g, '')"  />

          <label for="paisOrigen">País de Origen:</label>
          <select v-model="form.conyuge.paisOrigenClienteConyuge" id="paisOrigen">
            <option disabled value="">Seleccione un país</option>
            <option v-for="pais in paises" :key="pais.id" :value="pais.id">{{ pais.nombre }}</option>
          </select>

          <label for="paisResidencia">País de Residencia:</label>
          <select v-model="form.conyuge.paisResidenciaClienteConyuge" id="paisResidencia">
            <option disabled value="">Seleccione un país</option>
            <option v-for="residencia in residencias" :key="residencia.id" :value="residencia.id">{{ residencia.nombre }}</option>
          </select>

          <label for="departamento">Departamento:</label>
          <select v-model="form.conyuge.departamentoClienteConyuge" id="departamento">
            <option value="" disabled>Selecciona un departamento</option>
            <option v-for="departamento in departamentos" :key="departamento.id" :value="departamento.id">{{ departamento.nombre }}</option>
          </select>

          <label>Provincia:</label>
          <select v-model="form.conyuge.provinciaClienteConyuge">
            <option value="" disabled selected>Seleccione una provincia</option>
            <option v-for="provincia in provinciasFiltradasConyuge" :key="provincia.id" :value="provincia.id">{{ provincia.nombre }}</option>
          </select>

          <label>Distrito:</label>
          <select v-model="form.conyuge.distritoClienteConyuge">
            <option value="" disabled selected>Seleccione un distrito</option>
            <option v-for="distrito in distritosFiltradosConyuge" :key="distrito.id" :value="distrito.id">{{ distrito.nombre }}</option>
          </select>

          <label>Dirección:</label>
          <input v-model="form.conyuge.direccionClienteConyuge" type="text"  />

          <label>Correo Electrónico:</label>
          <div class="email-input">
            <input v-model="form.conyuge.correoUsuarioCliente" type="email" placeholder="usuario@dominio.com"  />
          </div>

          <label for="prefijoTelefonico">Número Telefónico:</label>
          <div style="display: flex; gap: 5px;">
            <select v-model="form.conyuge.prefijoTelefonicoClienteConyuge" id="prefijoTelefonico">
              <option v-for="prefijo in prefijos" :key="prefijo.id" :value="prefijo.id">{{ prefijo.codigo }}</option>
            </select>
            <input v-model="form.conyuge.numTelefonicoClienteConyuge" type="text" placeholder="Ingrese su número" @input="form.conyuge.numTelefonicoClienteConyuge = form.conyuge.numTelefonicoClienteConyuge.replace(/[^0-9]/g, '')"  />
          </div>

        </div>

        <button type="submit">Siguiente</button>
      </form>
      <form @submit.prevent="submitForm2">

        <h3>Información de Copropietarios</h3>

        <label>Número de Copropietarios:</label>
        <input v-model.number="form.numCopropietarios" type="number" min="0" @input="actualizarCopropietarios" />

        <div v-for="(copropietario, index) in form.copropietarios" :key="index">
          <h3>Copropietario {{ index + 1 }}</h3>

          <label>Nombre y Apellido:</label>
          <input v-model="copropietario.nombreCopropietarios" type="text" @input="copropietario.nombreCopropietarios = copropietario.nombreCopropietarios.replace(/[0-9]/g, '')" />


          <label>Ocupación:</label>
          <input type="text"
                 v-model="copropietario.ocupacionCopropietario"
                 placeholder="Ingrese su ocupación"
                 @input="copropietario.ocupacionCopropietario = copropietario.ocupacionCopropietario.replace(/[0-9]/g, '')">

          <label>Tipo de Identificación:</label>
          <select v-model="copropietario.tipoIdentificacionCopropietarios" id="tipoIdentificacion">
            <option v-for="tipo in tipoIdentificacion" :key="tipo.id" :value="tipo.id">
              {{ tipo.nombre }}
            </option>
          </select>

          <label>Número de Identificación:</label>
          <input v-model="copropietario.numIdentificacionCopropietarios" type="text" />

          <label for="paisOrigen">País de Origen:</label>
          <select v-model="copropietario.paisOrigenCopropietarios" id="paisOrigen">
            <option disabled value="">Seleccione un país</option>
            <option v-for="pais in paises" :key="pais.id" :value="pais.id">
              {{ pais.nombre }}
            </option>
          </select>

          <label>País de Residencia:</label>
          <select v-model="copropietario.paisResidenciaCopropietarios" id="paisResidencia">
            <option disabled value="">Seleccione un país</option>
            <option
                v-for="residencia in residencias"
                :key="residencia.id"
                :value="residencia.id"
            >
              {{ residencia.nombre }}
            </option>
          </select>

          <label for="departamento">Departamento:</label>
          <select v-model="copropietario.departamentoCopropietarios" id="departamento">
            <option value="" disabled>Selecciona un departamento</option>
            <option v-for="departamento in departamentos"
                    :key="departamento.id"
                    :value="departamento.id">
              {{ departamento.nombre }}
            </option>
          </select>

          <label>Provincia:</label>
          <select v-model="copropietario.provinciaCopropietarios">
            <option value="" disabled selected>Seleccione una provincia</option>
            <option v-for="provincia in provinciasFiltradasCopropietario" :key="provincia.id" :value="provincia.id">
              {{ provincia.nombre }}
            </option>
          </select>

          <label>Distrito:</label>
          <select v-model="copropietario.distritoCopropietarios">
            <option value="" disabled selected>Seleccione un distrito</option>
            <option v-for="distrito in distritosFiltradosCopropietario" :key="distrito.id" :value="distrito.id">
              {{ distrito.nombre }}
            </option>
          </select>

          <label>Dirección:</label>
          <input v-model="copropietario.direccionCopropietariosHogar" type="text" />

          <label>Correo Electrónico:</label>
          <input v-model="copropietario.correoUsuarioCopropietarios" type="email" placeholder="usuario@dominio.com" />

          <label for="prefijoTelefonico">Número Telefónico:</label>
          <div style="display: flex; gap: 5px;">
            <select v-model="copropietario.prefijoTelefonicoCopropietarios" id="prefijoTelefonico">
              <option v-for="prefijo in prefijos" :key="prefijo.id" :value="prefijo.id">{{ prefijo.codigo }}</option>
            </select>
            <input v-model="copropietario.numTelefonicoCopropietarios" type="text" placeholder="Ingrese su número" @input="copropietario.numTelefonicoCopropietarios = copropietario.numTelefonicoCopropietarios.replace(/[^0-9]/g, '')"/>
          </div>

          <label for="estadoCivil">Estado Civil:</label>
          <select v-model="copropietario.estadoCivilCopropietarios" id="estadoCivil">
            <option v-for="estado in estadoCivil" :key="estado.id" :value="estado.id">
              {{ estado.nombre }}
            </option>
          </select>


          <!-- Datos del CónyugeCOPROPIETARIO (solo si está casado) -->
          <div v-if="copropietario.estadoCivilCopropietarios === 2">

            <h3 class="titulodatoslotes">Datos del Cónyuge del Copropietario {{ index + 1 }}</h3>

            <label>Nombre y Apellido:</label>
            <input v-model="copropietario.conyuge.nombreCopropietariosConyuge" type="text"  @input="copropietario.conyuge.nombreCopropietariosConyuge = copropietario.conyuge.nombreCopropietariosConyuge.replace(/[0-9]/g, '')"  />

            <label>Ocupación:</label>
            <input type="text" v-model="copropietario.conyuge.ocupacionCopropietarioConyuge" placeholder="Ingrese su ocupación" @input="copropietario.conyuge.ocupacionCopropietarioConyuge = copropietario.conyuge.ocupacionCopropietarioConyuge.replace(/[0-9]/g, '')">

            <label>Tipo de Identificación:</label>
            <select v-model="copropietario.conyuge.tipoIdentificacionCopropietariosConyuge" id="tipoIdentificacion">
              <option v-for="tipo in tipoIdentificacion" :key="tipo.id" :value="tipo.id">{{ tipo.nombre }}</option>
            </select>

            <label>Número de Identificación:</label>
            <input v-model="copropietario.conyuge.numIdentificacionCopropietariosConyuge" type="text" />

            <label>País de Origen:</label>
            <select v-model="copropietario.conyuge.paisOrigenCopropietariosConyuge" id="paisOrigen">
              <option disabled value="">Seleccione un país</option>
              <option v-for="pais in paises" :key="pais.id" :value="pais.id">{{ pais.nombre }}</option>
            </select>

            <label>País de Residencia:</label>
            <select v-model="copropietario.conyuge.paisResidenciaCopropietariosConyuge" id="paisResidencia">
              <option disabled value="">Seleccione un país</option>
              <option v-for="residencia in residencias" :key="residencia.id" :value="residencia.id">{{ residencia.nombre }}</option>
            </select>

            <label for="departamento">Departamento:</label>
            <select v-model="copropietario.conyuge.departamentoCopropietariosConyuge" id="departamento">
              <option value="" disabled>Selecciona un departamento</option>
              <option v-for="departamento in departamentos"
                      :key="departamento.id"
                      :value="departamento.id">
                {{ departamento.nombre }}
              </option>
            </select>

            <label>Provincia:</label>
            <select v-model="copropietario.conyuge.provinciaCopropietariosConyuge">
              <option value="" disabled selected>Seleccione una provincia</option>
              <option v-for="provincia in provinciasFiltradasCopropietarioConyuge" :key="provincia.id" :value="provincia.id">{{ provincia.nombre }}</option>
            </select>

            <label>Distrito:</label>
            <select v-model="copropietario.conyuge.distritoCopropietariosConyuge">
              <option value="" disabled selected>Seleccione un distrito</option>
              <option v-for="distrito in distritosFiltradosCopropietarioConyuge" :key="distrito.id" :value="distrito.id">{{ distrito.nombre }}</option>
            </select>

            <label>Dirección:</label>
            <input v-model="copropietario.conyuge.direccionCopropietariosConyuge" type="text" />

            <label>Correo Electrónico:</label>
            <input v-model="copropietario.conyuge.correoUsuarioCopropietariosConyuge" type="email" placeholder="usuario@dominio.com" />

            <label for="prefijoTelefonico">Número Telefónico:</label>
            <div style="display: flex; gap: 5px;">
              <select v-model="copropietario.conyuge.prefijoTelefonicoCopropietariosConyuge" id="prefijoTelefonico">
                <option v-for="prefijo in prefijos" :key="prefijo.id" :value="prefijo.id">{{ prefijo.codigo }}</option>
              </select>
              <input v-model="copropietario.conyuge.numTelefonicoCopropietariosConyuge" type="text" placeholder="Ingrese su número" @input="copropietario.conyuge.numTelefonicoCopropietariosConyuge = copropietario.conyuge.numTelefonicoCopropietariosConyuge.replace(/[^0-9]/g, '')" />
            </div>

          </div>
        </div>


        <h3>Datos de Lotes</h3>

        <label>Número de Lotes Adquiridos:</label>
        <input v-model.number="form.numLotes" type="number" min="0" @change="actualizarLotes" />

        <div v-for="(lote, index) in form.lotes" :key="index">
          <h4>Lote {{ index + 1 }}</h4>

          <label>Proyecto:</label>
          <select v-model="lote.proyectolote">
            <option v-for="proyecto in proyectos" :key="proyecto.id" :value="proyecto.id">{{ proyecto.nombre }}</option>
          </select>

          <label>Ubicación de Lote:</label>
          <select v-model="lote.ubicacionLote">
            <option v-for="ubicacion in ubicaciones" :key="ubicacion.id" :value="ubicacion.id">{{ ubicacion.nombre }}</option>
          </select>

          <label>Manzana:</label>
          <input v-model="lote.manzanalote" type="text" />

          <label>Número de Lote:</label>
          <input v-model="lote.numerolote" type="text" @input="lote.numerolote = lote.numerolote.replace(/[^0-9]/g, '')"/>

          <label>Tipo de Contrato:</label>
          <select v-model="lote.tipoContratolote">
            <option v-for="tipo in tiposContrato" :key="tipo.id" :value="tipo.id">{{ tipo.nombre }}</option>
          </select>

          <label>Área del Lote m2:</label>
          <input v-model="lote.areaLote" type="text" @input="lote.areaLote = lote.areaLote.replace(/[^0-9]/g, '')" />

          <label>Alicuota(%):</label>
          <input v-model="lote.alicuotaLote" type="number" @input="lote.alicuotaLetraslote = numeroALetras(parseInt(lote.alicuotaLote) || 0)"/>

          <label>Alicuota en Letras:</label>
          <input v-model="lote.alicuotaLetraslote" type="text" readonly />

        </div>

        <button type="submit">Enviar</button>
      </form>
      <form @submit.prevent="submitLinderos">
        <div v-for="(lote, index) in form.lotes" :key="index">
          <h4>Lindero para Lote {{ index + 1 }}</h4>

          <label>Por la derecha(m):</label>
          <input v-model="lote.linderos.porLaDerechaLindero" type="number" />

          <label>Por la izquierda(m):</label>
          <input v-model="lote.linderos.porLaIzquierdaLindero" type="number" />

          <label>Por el frente(m):</label>
          <input v-model="lote.linderos.porElFrenteLindero" type="number" />

          <label>Por el fondo(m):</label>
          <input v-model="lote.linderos.porElFondoLindero" type="number" />
        </div>

        <button type="submit">Enviar</button>
      </form>

      <div v-if="formularioActual === 2 " class="overlay">
          <div class="modal">
            <h2 class="tituloformulario">Detalles de Matriz</h2>
            <div class="formulario-all">
              <form @submit.prevent="finalizarRegistroMatriz">
                <div v-for="(matriz, index) in form.lotes" :key="index">
                  <h3>Matriz {{ index + 1 }}</h3>

                  <label>Departamento:</label>
                  <select v-model="matriz.matriz.departamentoMatriz">
                    <option value="" disabled>Selecciona un departamento</option>
                    <option v-for="d in departamentos" :key="d.id" :value="d.id">
                      {{ d.nombre }}
                    </option>
                  </select>

                  <label>Provincia:</label>
                  <select v-model="matriz.matriz.provinciaMatriz">
                    <option value="" disabled>Selecciona una provincia</option>
                    <option
                        v-for="p in provincias.filter(p => p.departamentoId === matriz.matriz.departamentoMatriz)"
                        :key="p.id"
                        :value="p.id"
                    >
                      {{ p.nombre }}
                    </option>
                  </select>

                  <label>Distrito:</label>
                  <select v-model="matriz.matriz.distritoMatriz">
                    <option value="" disabled>Selecciona un distrito</option>
                    <option
                        v-for="d in distritos.filter(d => d.provinciaId === matriz.matriz.provinciaMatriz)"
                        :key="d.id"
                        :value="d.id"
                    >
                      {{ d.nombre }}
                    </option>
                  </select>


                  <label>Ubicación de Lote:</label>
                  <select v-model="matriz.matriz.ubicacionMatriz">
                    <option value="" disabled >Seleccione una ubicación</option>
                    <option v-for="ubicacion  in ubicaciones" :key="ubicacion.id" :value="ubicacion.id">{{ ubicacion.nombre }}</option>
                  </select>

                  <label for="areaMatrizHas">Area Matriz Has:</label>
                  <input id="areaMatrizHas" v-model.number="matriz.matriz.areaMatrizHasMatriz" type="number" min="0" required/>

                  <label for="Registros_DE">Registros DE:</label>
                  <input id="Registros_DE" v-model="matriz.matriz.registroDeMatriz" type="text"/>

                  <label for="Partida_Matriz">Partida Matriz:</label>
                  <input id="Partida_Matriz" v-model="matriz.matriz.partidaMatriz" type="text"/>

                  <label for="Unidad_Catastral">Unidad Catastral:</label>
                  <input id="Unidad_Catastral" v-model="matriz.matriz.unidadCatastralMatriz" type="text"/>

                  <label for="Urbanizacion_Matriz">Urbanizacion Matriz:</label>
                  <input id="Urbanizacion_Matriz" v-model="matriz.matriz.urbanizacionMatriz" type="text"/>

                  <label for="Compraventa_Matriz">Compraventa Matriz:</label>
                  <input id="Compraventa_Matriz" v-model="matriz.matriz.compraventaMatriz" type="text"/>

                  <label for="Situacion_Legal">Situacion Legal:</label>
                  <input id="Situacion_Legal" v-model="matriz.matriz.situacionLegalMatriz" type="text"/>
                </div>
                  <button type="submit" class="btn btn-primary">Finalizar Registro</button>
              </form>
                  <button @click="cerrarModal">Cerrar</button>
            </div>
          </div>
        </div>
      <div v-if="formularioActual === 3" class="overlay">
        <div class="modal">
          <h2 class="tituloformulario">Resumen del Registro</h2>

          <div class="formulario-all resumen-box">
            <!-- Sección Cliente -->
            <div class="seccion-cliente">
              <h3>Datos del Cliente</h3>
              <p><strong>Nombre y Apellido:</strong> {{ form.nombreCliente }}</p>
              <p><strong>Nacionalidad:</strong> {{ obtenerNombrePais(form.paisOrigen) }}</p>
              <p><strong>País de Residencia:</strong> {{  obtenerNombreResidencia(form.paisdeResidencia) }}</p>
              <p><strong>Departamento:</strong> {{ obtenerNombreDepartamento(form.departamento) }}</p>
              <p><strong>Provincia:</strong> {{ obtenerNombreProvincia(form.provincia) }}</p>
              <p><strong>Distrito:</strong> {{ obtenerNombreDistrito(form.distrito) }}</p>
              <p><strong>Código de Cliente Asignado:</strong> {{ form.idCliente }}</p>
              <p><strong>Número de Contratos:</strong> {{ form.lotes.length }}</p>
            </div>

            <!-- Sección Lotes -->
            <div class="seccion-lotes" v-if="form.lotes.length">
              <h3>Información de Lotes</h3>
              <div v-for="(lote, index) in form.lotes" :key="index" class="lote-box">
                <h4>Lote {{ index + 1 }}:</h4>
                <p><strong>Proyecto:</strong> {{ obtenerNombreProyecto(lote.proyectolote) }}</p>
                <p><strong>Manzana:</strong> {{ lote.manzanalote }}</p>
                <p><strong>Lote:</strong> {{ lote.numerolote }}</p>
              </div>
            </div>

            <!-- Sección Contacto -->
            <div class="seccion-contacto">
              <p><strong>Correo Electrónico:</strong> {{ form.correoUsuario }}</p>
              <p><strong>Teléfono:</strong> {{ form.numTelefonico }}</p>
            </div>

            <!-- Botón -->
            <div class="acciones">
              <button class="btn btn-secondary" @click="cerrarResumen">Cerrar</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
 </div>
</div>
</template>

<script setup>
import { ref, watch ,computed ,onMounted ,watchEffect } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';
import BarraSuperiorDashboard from "@/components/Dashboard/BarraSuperiorDashboard.vue";
import BarraLateralDashboard from "@/components/Dashboard/BarraLateralDashboard.vue";
import { paises } from '@/data/paises.js';
import { residencias } from '@/data/residencias'
import {prefijos} from "@/data/prefijos.js";
import { estadoCivil } from '@/data/estadoCivil.js';
import { tipoIdentificacion } from '@/data/tipoIdentificacion.js';
import { proyectos } from '@/data/proyectos.js';
import { tiposContrato } from '@/data/tiposContrato.js';
import { ubicaciones } from '@/data/ubicaciones.js'
import { departamentos } from '@/data/departamentos.js';
import { provincias } from '@/data/provincias.js';
import { distritos } from '@/data/distritos.js';



const router = useRouter();
const formularioActual = ref(1);
const idCliente=ref(null);
const form = ref({
  nombreCliente: '',
  ocupacionCliente: '',
  tipoIdentificacion: 1,
  numIdentificacionUsuario: '',
  paisOrigen: 8,
  paisdeResidencia: 8,
  departamento:'',
  provincia: '',
  distrito: '',
  direccion: '',
  correoUsuario: '',
  prefijoTelefonico: 8,
  numTelefonico: '',
  estadoCivil: 1,


  // Datos del cónyuge
  conyuge: {
    nombreClienteConyuge: '',
    ocupacionClienteConyuge: '',
    tipoIdentificacionClienteConyuge: 1,
    numIdentificacionClienteConyuge: '',
    paisOrigenClienteConyuge: 8,
    paisResidenciaClienteConyuge: 8,
    departamentoClienteConyuge: '',
    provinciaClienteConyuge: '',
    distritoClienteConyuge: '',
    direccionClienteConyuge: '',
    correoUsuarioCliente: '',
    prefijoTelefonicoClienteConyuge: 8,
    numTelefonicoClienteConyuge: '',
  },

    numCopropietarios: 0,
    copropietarios: [],
    numLotes: 0,
    lotes: []
});



const formularioClientevarios = async () => {
  try {

    const userData = JSON.parse(localStorage.getItem("user"));
    const idOperario = userData ? userData.idOperario : null;


    if (!idOperario) {
      console.error("No se encontró un ID de operario en localStorage.");
      return;
    }

    const clientePayload = {
      nombresApellidos: form.value.nombreCliente,
      ocupacion: form.value.ocupacionCliente,
      idIdentificacion: form.value.tipoIdentificacion,
      numeroIdentificacion: form.value.numIdentificacionUsuario,
      idNacionalidad: form.value.paisOrigen,
      idResidencia: form.value.paisdeResidencia,
      idDepartamento: form.value.departamento,
      idProvincia: form.value.provincia,
      idDistrito: form.value.distrito,
      direccion: form.value.direccion,
      correoElectronico: form.value.correoUsuario,
      idPrefijo: form.value.prefijoTelefonico,
      celularCliente: form.value.numTelefonico,
      idEstadoCivil: form.value.estadoCivil,
    };

    console.log("Datos del Cliente a enviar:", clientePayload);

    await axios.post("http://localhost:8080/api/clientes", clientePayload, {
      withCredentials: true,
      headers: {
        "Content-Type": "application/json",
        "X-User-ID": idOperario,
      },
    });

    const response = await axios.get("http://localhost:8080/api/clientes/ultimo");
    idCliente.value = response.data;
    console.log("ID del cliente asignado:", idCliente.value);

    if (form.value.estadoCivil === 2) {
      const conyugePayload = {
        idCliente: idCliente.value,
        ocupacionConyuge: form.value.conyuge.ocupacionClienteConyuge,
        idIdentificacionConyuge: form.value.conyuge.tipoIdentificacionClienteConyuge,
        numeroIdentificacionConyuge: form.value.conyuge.numIdentificacionClienteConyuge,
        idNacionalidadConyuge: form.value.conyuge.paisOrigenClienteConyuge,
        idResidenciaConyuge: form.value.conyuge.paisResidenciaClienteConyuge,
        idDepartamentoConyuge: form.value.conyuge.departamentoClienteConyuge,
        idProvinciaConyuge: form.value.conyuge.provinciaClienteConyuge,
        idDistritoConyuge: form.value.conyuge.distritoClienteConyuge,
        direccionConyuge: form.value.conyuge.direccionClienteConyuge,
        correoElectronicoConyuge: form.value.conyuge.correoUsuarioCliente,
        idPrefijoConyuge: form.value.conyuge.prefijoTelefonicoClienteConyuge,
        celularConyuge: form.value.conyuge.numTelefonicoClienteConyuge,
        nombresApellidosConyuge: form.value.conyuge.nombreClienteConyuge,
      };

      console.log("Datos del Cónyuge a enviar:", conyugePayload);

      await axios.post("http://localhost:8080/api/clienteConyuges", conyugePayload, {
        withCredentials: true,
        headers: {
          "Content-Type": "application/json",
          "X-User-ID": idOperario,
        },
      });

      console.log("Datos del cónyuge registrados con éxito.");
    }

  } catch (error) {
    console.error("Error al enviar los datos:", error.response ? error.response.data : error);
  }
};

onMounted(() => {
  const nombreGuardado = localStorage.getItem('nombreCompleto');
  const numeroDocumentoGuardado = localStorage.getItem('numeroDocumento');

  if (nombreGuardado) {
    form.value.nombreCliente = nombreGuardado;
  }

  if (numeroDocumentoGuardado) {
    form.value.numIdentificacionUsuario = numeroDocumentoGuardado;
  }
});


watch(() => form.value.numCopropietarios, (newVal) => {
  form.value.copropietarios = Array.from({ length: newVal }, () => ({
    nombreCopropietarios: '',
    ocupacionCopropietario: '',
    tipoIdentificacionCopropietarios: 1,
    numIdentificacionCopropietarios: '',
    paisOrigenCopropietarios: 8,
    paisResidenciaCopropietarios: 8,
    departamentoCopropietarios: '',
    provinciaCopropietarios: '',
    distritoCopropietarios: '',
    direccionCopropietarios: '',
    correoUsuarioCopropietarios: '',
    prefijoTelefonicoCopropietarios: 8,
    numTelefonicoCopropietarios: '',
    estadoCivilCopropietarios: 1,
    conyuge: {
      nombreCopropietariosConyuge: '',
      ocupacionCopropietarioConyuge: '',
      tipoIdentificacionCopropietariosConyuge: 1,
      numIdentificacionCopropietariosConyuge: '',
      distritoCopropietariosConyuge: '',
      provinciaCopropietariosConyuge: '',
      departamentoCopropietariosConyuge: '',
      paisOrigenCopropietariosConyuge: 8,
      paisResidenciaCopropietariosConyuge: 8,
      direccionCopropietariosConyuge: '',
      correoUsuarioCopropietariosConyuge: '',
      prefijoTelefonicoCopropietariosConyuge: 8,
      numTelefonicoCopropietariosConyuge: '',
    }
  }));
});


watch(() => form.value.numLotes, (newVal) => {
  form.value.lotes = Array.from({ length: newVal }, () => ({
    proyectolote:1,
    ubicacionLote: 1,
    manzanalote: '',
    numerolote: '',
    tipoContratolote: 1,
    areaLote: "",
    alicuotaLote: "",
    alicuotaLetraslote: "",
    matriz:{
      departamentoMatriz: '',
      provinciaMatriz: '',
      distritoMatriz: '',
      ubicacionMatriz: '',
      areaMatrizHas: "",
      registroDeMatriz: "",
      partidaMatriz: "",
      unidadCatastralMatriz: "",
      urbanizacionMatriz: "",
      compraventaMatriz: "",
      situacionLegalMatriz: "",
    },
    linderos:{
      porLaDerechaLindero: "",
      porLaIzquierdaLindero: "",
      porElFrenteLindero: "",
      porElFondoLindero: "",
    }
  }));
});

const submitForm2 = async () => {
  try {
    if (!idCliente.value) {
      console.error("Error: ID del cliente no encontrado.");
      return;
    }

    const userData = JSON.parse(localStorage.getItem("user"));
    const idOperario = userData ? userData.idOperario : null;

    if (!idOperario) {
      console.error("No se encontró un ID de operario en localStorage.");
      return;
    }

    const requests = [];

    if (form.value.numCopropietarios > 0) {
      form.value.copropietarios.forEach((copropietario) => {
        const copropietarioPayload = {
          idClienteCopropietarios: idCliente.value,
          nombresApellidosCopropietarios: copropietario.nombreCopropietarios,
          idIdentificacionCopropietarios: copropietario.tipoIdentificacionCopropietarios,
          numeroIdentificacionCopropietarios: copropietario.numIdentificacionCopropietarios,
          idNacionalidadCopropietarios: copropietario.paisOrigenCopropietarios,
          idResidenciaCopropietarios: copropietario.paisResidenciaCopropietarios,
          ocupacionCopropietarios: copropietario.ocupacionCopropietario,
          idDepartamentoCopropietarios: copropietario.departamentoCopropietarios,
          idProvinciaCopropietarios: copropietario.provinciaCopropietarios,
          idDistritoCopropietarios: copropietario.distritoCopropietarios,
          direccionCopropietarios: copropietario.direccionCopropietariosHogar,
          correoElectronicoCopropietarios: copropietario.correoUsuarioCopropietarios,
          idPrefijoCopropietarios: copropietario.prefijoTelefonicoCopropietarios,
          celularCopropietarios: copropietario.numTelefonicoCopropietarios,
          idEstadoCivilCopropietarios: copropietario.estadoCivilCopropietarios,
        };

        requests.push(
            axios.post("http://localhost:8080/api/copropietario", copropietarioPayload, {
              withCredentials: true,
              headers: {
                "Content-Type": "application/json",
                "X-User-ID": idOperario,
              },
            })
        );

        if (copropietario.estadoCivilCopropietarios === 2) {
          const copropietarioconyugePayload = {
            idClienteCopropietarioConyuge: idCliente.value,
            nombresApellidosCopropietarioConyuge: copropietario.conyuge.nombreCopropietariosConyuge,
            ocupacionCopropietarioConyuge: copropietario.conyuge.ocupacionCopropietarioConyuge,
            idIdentificacionCopropietarioConyuge: copropietario.conyuge.tipoIdentificacionCopropietariosConyuge,
            numeroIdentificacionCopropietarioConyuge: copropietario.conyuge.numIdentificacionCopropietariosConyuge,
            idDistritoCopropietarioConyuge: copropietario.conyuge.distritoCopropietariosConyuge,
            idProvinciaCopropietarioConyuge: copropietario.conyuge.provinciaCopropietariosConyuge,
            idDepartamentoCopropietarioConyuge: copropietario.conyuge.departamentoCopropietariosConyuge,
            idNacionalidadCopropietarioConyuge: copropietario.conyuge.paisOrigenCopropietariosConyuge,
            idResidenciaCopropietarioConyuge: copropietario.conyuge.paisResidenciaCopropietariosConyuge,
            direccionCopropietarioConyuge: copropietario.conyuge.direccionCopropietariosConyuge,
            correoElectronicoCopropietarioConyuge: copropietario.conyuge.correoUsuarioCopropietariosConyuge,
            idPrefijoCopropietarioConyuge: copropietario.conyuge.prefijoTelefonicoCopropietariosConyuge,
            celularCopropietarioConyuge: copropietario.conyuge.numTelefonicoCopropietariosConyuge,
          };
          requests.push(
              axios.post("http://localhost:8080/api/copropietarioconyuge", copropietarioconyugePayload, {
                withCredentials: true,
                headers: {
                  "Content-Type": "application/json",
                  "X-User-ID": idOperario,
                }
              })
          );
        }
      });
    }

    if (form.value.numLotes > 0) {
      for (const lote of form.value.lotes) {
        const lotePayload = {
          idClienteLote: idCliente.value,
          idTipoProyecto: lote.proyectolote,
          idUbicacion: lote.ubicacionLote,
          manzana: lote.manzanalote,
          numeroLote: lote.numerolote,
          idTipoContrato: lote.tipoContratolote,
          areaLote: lote.areaLote,
          alicuota: lote.alicuotaLote,
          alicuotaLetras: lote.alicuotaLetraslote,
        };

        await axios.post("http://localhost:8080/api/lotes", lotePayload, {
          withCredentials: true,
          headers: {
            "Content-Type": "application/json",
            "X-User-ID": idOperario,
          },
        });

        // Obtener el último ID de lote registrado desde el backend
        const { data: idLote } = await axios.get("http://localhost:8080/api/lotes/ultimo");

        // Almacenar el idLote en el objeto del lote
        lote.idLote = idLote;
      }

    }

    await Promise.all(requests);

    console.log("Copropietarios y lotes registrados con éxito.");

  } catch (error) {
    console.error("Error al enviar copropietarios y lotes:", error);
  }
};

const submitLinderos= async() =>{
  try {
    const requests = form.value.lotes.map(lote => {
      const LinderoLoteDTO = {
        idLote: lote.idLote,
        porLaDerecha: lote.linderos.porLaDerechaLindero,
        porLaIzquierda: lote.linderos.porLaIzquierdaLindero,
        porElFrente: lote.linderos.porElFrenteLindero,
        porElFondo: lote.linderos.porElFondoLindero,
      };

      return axios.post('http://localhost:8080/api/lindero', LinderoLoteDTO);
    });

    await Promise.all(requests);

    console.log('Lindero registrado con éxito.');

    formularioActual.value = 2;
  } catch (error) {
    console.error('Error en el registro de Lindero:', error);
  }
};

const finalizarRegistroMatriz = async () => {
  const confirmacion = window.confirm("¿Estás seguro de que todos los datos están correctos?");
  if (!confirmacion) {
    return;
  }

  try {
    const requests = form.value.lotes.map(lote => {
      const matrizLoteDTO = {
        idLote: lote.idLote,
        idDistrito: lote.matriz.distritoMatriz,
        idProvincia: lote.matriz.provinciaMatriz,
        idDepartamento: lote.matriz.departamentoMatriz,
        idUbicacion: lote.matriz.ubicacionMatriz,
        areaMatrizHas: lote.matriz.areaMatrizHasMatriz,
        registrosDE: lote.matriz.registroDeMatriz,
        partidaMatriz: lote.matriz.partidaMatriz,
        unidadCatastral: lote.matriz.unidadCatastralMatriz,
        urbanizacionMatriz: lote.matriz.urbanizacionMatriz,
        compraventaMatriz: lote.matriz.compraventaMatriz,
        situacionLegal: lote.matriz.situacionLegalMatriz,

      };

      return axios.post('http://localhost:8080/api/matrices', matrizLoteDTO);
    });

    await Promise.all(requests);
    alert('Registro completado exitosamente');
    console.log('Matriz registrada con éxito.');


    formularioActual.value = 3;
  } catch (error) {
    console.error('Error en el registro:', error);
    alert('Ocurrió un error al enviar los detalles del lote.');
  }
};

const cerrarModal = () => {
  formularioActual.value = 0;
};
const cerrarResumen = () => {
  router.push("/dashboard/formularios/registro-cliente");
};


//-------------------------------------

// Provincias filtradas por departamento seleccionado
const provinciasFiltradas = computed(() =>
    provincias.filter(p => p.departamentoId === form.value.departamento)
);

// Cuando cambia el departamento, seleccionar la primera provincia automáticamente
watch(() => form.value.departamento, () => {
  const primeraProvincia = provinciasFiltradas.value[0];
  form.value.provincia = primeraProvincia ? primeraProvincia.id : '';
  form.value.distrito = ''; // resetear distrito al cambiar de departamento
});

// Distritos filtrados por provincia seleccionada
const distritosFiltrados = computed(() =>
    distritos.filter(d => d.provinciaId === form.value.provincia)
);

// Cuando cambia la provincia, seleccionar el primer distrito automáticamente
watch(() => form.value.provincia, () => {
  const primerDistrito = distritosFiltrados.value[0];
  form.value.distrito = primerDistrito ? primerDistrito.id : '';
});
//-------------------------------------------------------------------

const distritosFiltradosConyuge = computed(() =>
    distritos.filter(distrito => distrito.provinciaId === form.value.conyuge.provinciaClienteConyuge)
);

watch(() => form.value.conyuge.provinciaClienteConyuge, () => {
  const primerDistritoConyuge = distritosFiltradosConyuge.value[0];
  form.value.conyuge.distritoClienteConyuge = primerDistritoConyuge ? primerDistritoConyuge.id : '';
});

const provinciasFiltradasConyuge = computed(() =>
    provincias.filter(provincia => provincia.departamentoId === form.value.conyuge.departamentoClienteConyuge)
);

watch(() => form.value.conyuge.departamentoClienteConyuge, () => {
  const primeraProvinciaConyuge = provinciasFiltradasConyuge.value[0];
  form.value.conyuge.provinciaClienteConyuge = primeraProvinciaConyuge ? primeraProvinciaConyuge.id : '';
});

// //---------------------------------------------------------------

const distritosFiltradosCopropietario = computed(() => {
  if (!form.value.copropietarios.length) return [];
  return distritos.filter(distrito => distrito.provinciaId === form.value.copropietarios[0].provinciaCopropietarios);
});

watch(() => form.value.copropietarios[0]?.provinciaCopropietarios, () => {
  if (!form.value.copropietarios.length) return;
  const primerDistritoCopropietario = distritosFiltradosCopropietario.value[0];
  form.value.copropietarios[0].distritoCopropietarios = primerDistritoCopropietario ? primerDistritoCopropietario.id : '';
});

const provinciasFiltradasCopropietario = computed(() => {
  if (!form.value.copropietarios.length) return [];
  return provincias.filter(provincia => provincia.departamentoId === form.value.copropietarios[0].departamentoCopropietarios);
});

watch(() => form.value.copropietarios[0]?.departamentoCopropietarios, () => {
  if (!form.value.copropietarios.length) return;
  const primeraProvinciaCopropietario = provinciasFiltradasCopropietario.value[0];
  form.value.copropietarios[0].provinciaCopropietarios = primeraProvinciaCopropietario ? primeraProvinciaCopropietario.id : '';
});

// //----------------------------------------------

const distritosFiltradosCopropietarioConyuge = computed(() => {
  if (!form.value.copropietarios.length) return [];
  return distritos.filter(distrito =>
      distrito.provinciaId === form.value.copropietarios[0].conyuge.provinciaCopropietariosConyuge
  );
});

watch(() => form.value.copropietarios[0]?.conyuge.provinciaCopropietariosConyuge, () => {
  if (!form.value.copropietarios.length) return;
  const primerDistritoCopropietarioConyuge = distritosFiltradosCopropietarioConyuge.value[0];
  form.value.copropietarios[0].conyuge.distritoCopropietariosConyuge =
      primerDistritoCopropietarioConyuge ? primerDistritoCopropietarioConyuge.id : '';
});

const provinciasFiltradasCopropietarioConyuge = computed(() => {
  if (!form.value.copropietarios.length) return [];
  return provincias.filter(provincia =>
      provincia.departamentoId === form.value.copropietarios[0].conyuge.departamentoCopropietariosConyuge
  );
});

watch(() => form.value.copropietarios[0]?.conyuge.departamentoCopropietariosConyuge, () => {
  if (!form.value.copropietarios.length) return;
  const primeraProvinciaCopropietarioConyuge = provinciasFiltradasCopropietarioConyuge.value[0];
  form.value.copropietarios[0].conyuge.provinciaCopropietariosConyuge =
      primeraProvinciaCopropietarioConyuge ? primeraProvinciaCopropietarioConyuge.id : '';
});

// //--------------------

function numeroALetras(numero) {
  const unidades = ['', 'uno', 'dos', 'tres', 'cuatro', 'cinco', 'seis', 'siete', 'ocho', 'nueve'];
  const especiales = ['diez', 'once', 'doce', 'trece', 'catorce', 'quince', 'dieciséis', 'diecisiete', 'dieciocho', 'diecinueve'];
  const decenas = ['', '', 'veinte', 'treinta', 'cuarenta', 'cincuenta', 'sesenta', 'setenta', 'ochenta', 'noventa'];
  const centenas = ['', 'ciento', 'doscientos', 'trescientos', 'cuatrocientos', 'quinientos', 'seiscientos', 'setecientos', 'ochocientos', 'novecientos'];

  if (numero === 0) return 'cero';
  if (numero === 100) return 'cien';

  let letras = '';

  const miles = Math.floor(numero / 1000);
  const resto = numero % 1000;

  // Miles
  if (miles > 0) {
    if (miles === 1) {
      letras += 'mil ';
    } else {
      letras += convertirMenorA1000(miles) + ' mil ';
    }
  }

  // Resto
  if (resto > 0) {
    letras += convertirMenorA1000(resto);
  }

  return letras.trim();

  function convertirMenorA1000(num) {
    if (num === 0) return '';
    if (num === 100) return 'cien';

    const c = Math.floor(num / 100);
    const d = Math.floor((num % 100) / 10);
    const u = num % 10;

    let resultado = '';
    if (c > 0) {
      resultado += centenas[c] + ' ';
    }

    const dosDigitos = num % 100;
    if (dosDigitos < 10) {
      resultado += unidades[dosDigitos];
    } else if (dosDigitos < 20) {
      resultado += especiales[dosDigitos - 10];
    } else {
      resultado += decenas[d];
      if (u !== 0) {
        resultado += ' y ' + unidades[u];
      }
    }

    return resultado.trim();
  }
}

const obtenerNombreResidencia = (id) => {
  const item = residencias.find(n => n.id === id);
  return item ? item.nombre : 'Desconocido';
};

const obtenerNombrePais = (id) => {
  const item = paises.find(p => p.id === id);
  return item ? item.nombre : 'Desconocido';
};

const obtenerNombreDepartamento = (id) => {
  const item = departamentos.find(d => d.id === id);
  return item ? item.nombre : 'Desconocido';
};

const obtenerNombreProvincia = (id) => {
  const item = provincias.find(p => p.id === id);
  return item ? item.nombre : 'Desconocido';
};

const obtenerNombreDistrito = (id) => {
  const item = distritos.find(d => d.id === id);
  return item ? item.nombre : 'Desconocido';
};

const obtenerNombreProyecto = (id) => {
  const proyecto = proyectos.find(p => p.id === id);
  return proyecto ? proyecto.nombre : 'Desconocido';
};



</script>

<style scoped>

/* BACKGROUND */

.container {
  background-image: url("@/assets/imagenes/FondoDashboard.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  width: 125vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.nav-buttons button {
  margin: 5px;
  padding: 8px 12px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}
.nav-buttons button:hover {
  background-color: #0056b3;
}


.user-icon img {
  height: 40px;
  width: 40px;
  border-radius: 50%;
}
.logo img {
  height: 50px;
}
.tituloformulario{
  font-size: 24px;
  font-weight: bold;
  margin-top: 20px;
  text-align: center;
  color:black;
}


/*STYLE FORMULARIO 1*/
.formulario-all{

  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  margin: auto;
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-height: 80vh; /* Altura máxima para evitar que sobresalga */
  overflow-y: auto;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
}

input, select {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.email-input {
  width: 90%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}



button {
  background-color: #007bff;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
h3{
  text-align: center;
}


/* FORMULARIO 2  */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(50, 50, 50, 0.7); /* Fondo plomo oscuro translúcido */
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000; /* el modal esté sobre */
  backdrop-filter: blur(5px); /* Efecto de desenfoque */
  animation: fade-in 0.3s ease-in-out;
}

/* 🔹 CONTENEDOR DEL MODAL 🔹 */
.modal {
  background: white;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.3);
  width: 380px;
  max-width: 90%;
  text-align: center;
  position: relative;
  transform: scale(0.9);
  animation: scale-in 0.3s ease-in-out forwards;
}

/* 🔹 ANIMACIONES PARA UNA TRANSICIÓN SUAVE 🔹 */
@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes scale-in {
  from {
    transform: scale(0.9);
  }
  to {
    transform: scale(1);
  }
}



/* 🔹 MEJORAS EN EL FORMULARIO 🔹 */
.modal form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.modal label {
  font-weight: bold;
  text-align: left;
  display: block;
  color: #333;
}

.modal input,
.modal select {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 14px;
}

/* 🔹 BOTÓN "FINALIZAR REGISTRO" 🔹 */
.modal button[type="submit"] {
  background: #007bff;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
  transition: background 0.3s ease;
}

.modal button[type="submit"]:hover {
  background: #0056b3;
}
</style>
