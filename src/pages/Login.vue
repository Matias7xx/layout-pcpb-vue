<template>
  <div class="min-h-screen flex flex-col sm:justify-center items-center pt-6 sm:pt-0 bg-gradient-to-b from-gray-50 to-gray-200">
    <!-- Background -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute -top-20 -right-20 w-96 h-96 rounded-full opacity-10 blur-3xl"></div>
      <div class="absolute -bottom-20 -left-20 w-96 h-96 rounded-full opacity-10 blur-3xl"></div>
    </div>
    
    <!-- Logo -->
    <div ref="logoRef" class="relative z-10 mb-8 flex flex-col items-center">
        <img 
            src="/img/logo-pc.png" 
            alt="Logo PCPB" 
            class="w-32 sm:w-40 h-auto drop-shadow-lg flex-shrink-0"
          />
      
      <div class="mt-3 text-center">
        <h1 class="text-xl sm:text-2xl font-bold text-gray-800">Nome do Sistema</h1>
      </div>
    </div>

    <!-- Card de Login -->
    <div 
      ref="cardRef"
      class="animate-in w-full max-w-md px-6 py-8 bg-white shadow-xl overflow-hidden sm:rounded-lg relative z-10 border border-gray-200"
    >      
      
      <div v-if="status" class="mb-6 p-4 bg-green-50 rounded-lg text-green-700 text-sm">
        {{ status }}
      </div>

      <form @submit.prevent="handleSubmit" class="space-y-6">
        <!-- Matrícula -->
        <div class="animate-in relative">
          <label for="matricula" class="block text-sm font-medium text-gray-700 mb-2">
            Matrícula
          </label>
          <div class="mt-1 relative">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <!-- Ícone de badge -->
              <svg class="h-5 w-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H5a2 2 0 00-2 2v9a2 2 0 002 2h14a2 2 0 002-2V8a2 2 0 00-2-2h-5m-4 0V5a2 2 0 114 0v1m-4 0a2 2 0 104 0m-5 8a2 2 0 100-4 2 2 0 000 4zm0 0c1.306 0 2.417.835 2.83 2M9 14a3.001 3.001 0 00-2.83 2M15 11h3m-3 4h2" />
              </svg>
            </div>
            <input
              id="matricula"
              v-model="form.matricula"
              type="text"
              :class="[
                'pl-10 pr-4 block w-full border rounded-md shadow-sm transition-colors duration-200 py-3',
                errors.matricula 
                  ? 'border-red-300 focus:border-red-500 focus:ring-red-500' 
                  : 'border-gray-300'
              ]"
              required
              autofocus
              placeholder="Informe sua Matrícula"
              maxlength="7"
              minlength="7"
            />
          </div>
          <div v-if="errors.matricula" class="mt-2 text-sm text-red-600">
            {{ errors.matricula }}
          </div>
        </div>

        <!-- Senha -->
        <div class="animate-in relative">
          <label for="password" class="block text-sm font-medium text-gray-700 mb-2">
            Senha
          </label>
          <div class="mt-1 relative">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <!-- Ícone de cadeado -->
              <svg class="h-5 w-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
              </svg>
            </div>
            <input
              id="password"
              v-model="form.password"
              :type="showPassword ? 'text' : 'password'"
              :class="[
                'pl-10 pr-10 block w-full border rounded-md shadow-sm transition-colors duration-200 py-3',
                errors.password 
                  ? 'border-red-300 focus:border-red-500 focus:ring-red-500' 
                  : 'border-gray-300'
              ]"
              required
              placeholder="••••••••"
            />
            <button 
              type="button" 
              @click="togglePasswordVisibility" 
              class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 focus:outline-none"
            >
              <!-- Ícone de olho -->
              <svg v-if="showPassword" class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21" />
              </svg>
              <svg v-else class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
              </svg>
            </button>
          </div>
          <div v-if="errors.password" class="mt-2 text-sm text-red-600">
            {{ errors.password }}
          </div>
        </div>

        <!-- Lembrar-me -->
        <div class="animate-in block">
          <label class="flex items-center">
            <input 
              v-model="form.remember" 
              type="checkbox" 
              class="rounded border-gray-300 h-4 w-4" 
            />
            <span class="ml-2 text-sm text-gray-600">Lembrar-me</span>
          </label>
        </div>

        <!-- Botão de Login e Esqueci a Senha -->
        <div class="animate-in flex flex-col sm:flex-row items-center justify-between mt-6 space-y-4 sm:space-y-0">
          <button 
            type="button"
            class="text-sm text-gray-600 hover:text-[#bea55a] underline transition-colors duration-200"
            @click="handleForgotPassword"
          >
            Esqueceu sua senha?
          </button>

          <button 
            type="submit"
            :class="[
              'w-full sm:w-auto flex items-center justify-center space-x-2 px-8 py-3 bg-[#bea55a] text-white font-medium rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-[#bea55a] transition-all duration-200',
              isLoading 
                ? 'opacity-75 cursor-not-allowed' 
                : 'hover:bg-[#d4bf7a] hover:shadow-lg transform hover:-translate-y-0.5'
            ]"
            :disabled="isLoading"
          >
            <!-- Spinner de loading -->
            <svg 
              v-if="isLoading" 
              class="animate-spin h-4 w-4 text-white mr-2" 
              fill="none" 
              viewBox="0 0 24 24"
            >
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            <span>{{ isLoading ? 'Entrando...' : 'Entrar' }}</span>
          </button>
        </div>
      </form>
    </div>
    
    <!-- Rodapé -->
    <div class="animate-in mt-8 text-center">
      <div class="text-sm text-gray-600">
        © {{ currentYear }} Polícia Civil da Paraíba - Todos os direitos reservados
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'
import { useRouter } from 'vue-router'

// Composables
const router = useRouter()

// Estado reativo
const form = reactive({
  matricula: '',
  password: '',
  remember: false
})

const errors = reactive({})
const status = ref('')
const isLoading = ref(false)
const showPassword = ref(false)
const currentYear = new Date().getFullYear()

// Refs dos elementos
const logoRef = ref(null)
const cardRef = ref(null)

// Métodos
const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value
}

const validateForm = () => {
  // Limpar erros anteriores
  Object.keys(errors).forEach(key => delete errors[key])
  
  if (!form.matricula || form.matricula.length !== 7) {
    errors.matricula = 'A matrícula deve ter exatamente 7 caracteres'
  }
  
  if (!form.password || form.password.length < 6) {
    errors.password = 'A senha deve ter pelo menos 6 caracteres'
  }
  
  return Object.keys(errors).length === 0
}

const handleSubmit = async () => {
  if (!validateForm()) return
  
  isLoading.value = true
  
  try {
    // Simulação de login - substitua pela sua lógica de autenticação
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Aqui ocorre a chamada para a API de login
    console.log('Login realizado:', form)
    
    // Exemplo de redirecionamento após login bem sucedido
    // router.push('/dashboard')
    status.value = 'Login realizado com sucesso!'
    
  } catch (error) {
    console.error('Erro no login:', error)
    status.value = 'Erro ao realizar login. Tente novamente.'
  } finally {
    isLoading.value = false
  }
}

const handleForgotPassword = () => {
  // Implementar lógica de esqueci minha senha
  alert('Implementar funcionalidade de recuperação de senha')
}

// Animações de entrada
onMounted(() => {
  const elements = document.querySelectorAll('.animate-in')
  elements.forEach((el, index) => {
    setTimeout(() => {
      el.classList.add('animate-in-active')
    }, index * 100)
  })
})
</script>

<style scoped>
/* Animação de entrada */
.animate-in {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s ease-out;
}

.animate-in-active {
  opacity: 1;
  transform: translateY(0);
}

/* Animação de loading */
@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.animate-spin {
  animation: spin 1s linear infinite;
}

/* Efeitos de hover nos elementos */
button, a {
  transition: all 0.2s ease-in-out;
}

/* visual para campos de formulário */
input:focus {
  outline: none;
  box-shadow: 0 0 0 2px rgba(234, 179, 8, 0.25);
}

/* Responsividade */
@media (max-width: 640px) {
  .max-w-md {
    max-width: 90%;
  }
}

/* Acessibilidade */
@media (prefers-reduced-motion: reduce) {
  .animate-in,
  .animate-spin,
  button,
  a {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
</style>