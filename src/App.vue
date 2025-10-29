<template>
  <main class="min-h-screen bg-gradient-to-b from-slate-50 to-white text-slate-900">
    <div class="max-w-6xl mx-auto px-6 md:px-12 lg:px-24 py-10 space-y-12">
      <!-- HERO -->
      <section>
        <div class="text-center">
          <span class="inline-flex items-center gap-2 text-sm px-2.5 py-1 rounded-full bg-slate-100">
            <Sparkles class="w-4 h-4"/> Padrão de Informação 2035
          </span>
          <h1 class="mt-4 text-3xl md:text-5xl font-semibold leading-tight tracking-tight">
            Informação mínima para <span class="underline decoration-wavy decoration-sky-400">máxima ação</span>
          </h1>
          <p class="mt-4 text-slate-600 max-w-3xl mx-auto">
            Um modelo de apresentação otimizada: contextual, adaptativa, multimodal e curada. Feito para reduzir carga cognitiva e acelerar decisões.
          </p>

          <div class="mt-6 flex flex-wrap items-center justify-center gap-3">
            <button class="rounded-2xl px-4 py-2 bg-slate-900 text-white inline-flex items-center gap-2" @click="dialogAberto = true">
              <Play class="w-4 h-4"/> Ver demo de 30s
            </button>
            <button class="rounded-2xl px-4 py-2 border inline-flex items-center gap-2">
              <BookOpen class="w-4 h-4"/> Guia de design cognitivo
            </button>
          </div>
        </div>
      </section>

      <!-- DIALOG -->
      <transition name="fade">
        <div v-if="dialogAberto" class="fixed inset-0 z-50 grid place-items-center bg-black/30 p-4" @click.self="dialogAberto=false">
          <div class="w-full max-w-[640px] rounded-2xl bg-white p-6 shadow-lg">
            <div class="flex items-center justify-between mb-3">
              <h2 class="text-lg font-medium">Resumo em 30 segundos</h2>
              <button class="text-slate-500 hover:text-slate-700" @click="dialogAberto=false">✕</button>
            </div>
            <div class="prose prose-slate max-w-none">
              <p class="text-lg leading-relaxed">{{ resumo30s }}</p>
            </div>
          </div>
        </div>
      </transition>

      <!-- CONTROLES COGNITIVOS -->
      <section>
        <div class="grid md:grid-cols-3 gap-6">
          <!-- Foco & Densidade -->
          <article class="rounded-2xl shadow-sm border bg-white">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><Focus class="w-4 h-4"/> Foco & Densidade</h3>
            </header>
            <div class="p-4 space-y-4">
              <p class="text-sm text-slate-600">Controle o quanto ver: do ultrarresumo ao modo detalhado.</p>
              <div>
                <input type="range" min="0" max="100" step="10" v-model.number="densidade" class="w-full"/>
                <div class="text-xs text-slate-500 mt-2">Nível atual: {{ densidade }}%</div>
              </div>
              <label class="flex items-center justify-between cursor-pointer select-none">
                <span class="text-sm">Modo leitura profunda</span>
                <input type="checkbox" v-model="modoProfundo" class="peer sr-only">
                <span class="w-10 h-6 rounded-full bg-slate-300 peer-checked:bg-sky-500 relative transition">
                  <span class="absolute top-0.5 left-0.5 w-5 h-5 bg-white rounded-full shadow transition peer-checked:translate-x-4"></span>
                </span>
              </label>
            </div>
          </article>

          <!-- Adaptação por Perfil -->
          <article class="rounded-2xl shadow-sm border bg-white">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><Brain class="w-4 h-4"/> Adaptação por Perfil</h3>
            </header>
            <div class="p-4 space-y-3">
              <p class="text-sm text-slate-600">Selecione seu objetivo e receba apenas o necessário.</p>
              <div class="grid grid-cols-3 rounded-xl border overflow-hidden">
                <button :class="aba==='acao' ? abaOn : abaOff" @click="aba='acao'">Ação</button>
                <button :class="aba==='aprendizado' ? abaOn : abaOff" @click="aba='aprendizado'">Aprendizado</button>
                <button :class="aba==='auditoria' ? abaOn : abaOff" @click="aba='auditoria'">Auditoria</button>
              </div>
              <p v-if="aba==='acao'" class="text-sm text-slate-700">Checklist minimalista e playbooks prontos.</p>
              <p v-else-if="aba==='aprendizado'" class="text-sm text-slate-700">Mapas conceituais e simulações curtas.</p>
              <p v-else class="text-sm text-slate-700">Evidências, métricas e trilhas de decisão.</p>
            </div>
          </article>

          <!-- Curadoria & Sinal -->
          <article class="rounded-2xl shadow-sm border bg-white">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><BarChart4 class="w-4 h-4"/> Curadoria & Sinal</h3>
            </header>
            <div class="p-4 space-y-3">
              <p class="text-sm text-slate-600">Remoção de redundâncias e consolidação de aprendizados.</p>
              <ul class="text-sm list-disc ml-5 space-y-1">
                <li>Consolida versões e destaca diferenças.</li>
                <li>Promove conteúdo com maior impacto.</li>
                <li>Arquiva o resto com recuperação sob demanda.</li>
              </ul>
            </div>
          </article>
        </div>
      </section>

      <!-- RESUMO + ASSISTENTE -->
      <section>
        <div class="grid lg:grid-cols-3 gap-6">
          <article class="rounded-2xl shadow-sm border bg-white lg:col-span-2">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><Clock class="w-4 h-4"/> Resumo em 30s</h3>
            </header>
            <div class="p-4">
              <p class="text-lg leading-relaxed">{{ resumo30s }}</p>
              <div class="mt-4 flex gap-2">
                <span class="px-2 py-1 text-xs rounded-full bg-slate-100">Gestão primeiro</span>
                <span class="px-2 py-1 text-xs rounded-full bg-slate-100">Risco → ação</span>
                <span class="px-2 py-1 text-xs rounded-full bg-slate-100">Carga cognitiva baixa</span>
              </div>
            </div>
          </article>

          <article class="rounded-2xl shadow-sm border bg-white">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><Bot class="w-4 h-4"/> Assistente Contextual</h3>
            </header>
            <div class="p-4 space-y-3">
              <p class="text-sm text-slate-600">Converse para obter exatamente o que precisa.</p>
              <div class="flex items-center gap-2">
                <input class="w-full border rounded-xl px-3 py-2" placeholder="Pergunte algo… ex: gerar checklist" v-model="pergunta"/>
                <button class="rounded-xl px-3 py-2 bg-slate-900 text-white"><Wand2 class="w-4 h-4"/></button>
              </div>
              <p class="text-xs text-slate-500">Sugestões: “Resuma por papel”, “Mostrar lacunas”, “Exportar plano”.</p>
            </div>
          </article>
        </div>
      </section>

      <!-- MICRO-NARRATIVA + SIMULAÇÃO -->
      <section>
        <div class="grid lg:grid-cols-3 gap-6">
          <article class="rounded-2xl shadow-sm border bg-white lg:col-span-1">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><BookOpen class="w-4 h-4"/> Micro‑narrativa</h3>
            </header>
            <div class="p-4">
              <h4 class="font-medium text-slate-800">{{ microHistoria.titulo }}</h4>
              <p class="text-sm text-slate-600 mt-2">{{ microHistoria.narrativa }}</p>
              <div class="mt-3 text-xs text-slate-500">Lição: gestão reduz decisões ruins quando a pressão é alta.</div>
            </div>
          </article>

          <article class="rounded-2xl shadow-sm border bg-white lg:col-span-2">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><Play class="w-4 h-4"/> Simulação interativa (conceito)</h3>
            </header>
            <div class="p-4 space-y-3">
              <div class="w-full h-48 bg-gradient-to-br from-slate-100 to-slate-50 rounded-xl grid place-items-center text-sm text-slate-500">
                (Área para visual interativo/RA — evento → impacto → mitigação)
              </div>
              <div class="flex flex-wrap gap-2">
                <span class="px-2 py-1 text-xs rounded-full bg-slate-100">Propagação</span>
                <span class="px-2 py-1 text-xs rounded-full bg-slate-100">Isolamento</span>
                <span class="px-2 py-1 text-xs rounded-full bg-slate-100">Recuperação</span>
              </div>
            </div>
          </article>
        </div>
      </section>

      <!-- CHECKLIST -->
      <section>
        <article class="rounded-2xl shadow-sm border bg-white">
          <header class="p-4 border-b flex flex-col md:flex-row md:items-center md:justify-between gap-3">
            <h3 class="text-base flex items-center gap-2"><Search class="w-4 h-4"/> Checklist de Ação (filtrável)</h3>
            <div class="flex items-center gap-3">
              <input class="w-64 border rounded-xl px-3 py-2" placeholder="Filtrar por palavra‑chave…" v-model="filtro"/>
              <span class="px-2 py-1 text-xs rounded-full border cursor-help">Priorize pelo impacto</span>
            </div>
          </header>
          <div class="p-4">
            <div class="grid md:grid-cols-2 gap-3">
              <transition-group name="list" tag="div" class="contents">
                <div v-for="p in passosFiltrados" :key="p.id" class="p-4 rounded-xl border flex items-start gap-3" :class="p.impacto==='alto' ? 'border-sky-200 bg-sky-50' : 'border-slate-200 bg-white'">
                  <button @click="alternarChecklist(p.id)" class="mt-0.5 rounded-full border w-5 h-5 grid place-items-center" :class="itensConcluidos.includes(p.id) ? 'bg-sky-500 text-white border-sky-500' : 'border-slate-300'">
                    <Check v-if="itensConcluidos.includes(p.id)" class="w-3 h-3"/>
                  </button>
                  <div class="text-sm">
                    <div class="font-medium text-slate-800 flex items-center gap-2">
                      {{ p.texto }}
                      <span class="px-2 py-0.5 text-[10px] rounded bg-slate-100 capitalize">{{ p.impacto }}</span>
                    </div>
                    <div class="text-xs text-slate-500 mt-1">Dica: mantenha evidência mínima e mensurável.</div>
                  </div>
                </div>
              </transition-group>
            </div>
          </div>
        </article>
      </section>

      <!-- MAPA DE RISCOS -->
      <section>
        <article class="rounded-2xl shadow-sm border bg-white">
          <header class="p-4 border-b flex flex-col md:flex-row md:items-center md:justify-between gap-3">
            <h3 class="text-base flex items-center gap-2"><AlertTriangle class="w-4 h-4"/> Mapa de Riscos</h3>
            <div class="flex items-center gap-4">
              <div class="flex items-center gap-2">
                <span class="px-2 py-1 text-xs rounded-full border">Score mínimo</span>
                <div class="w-48">
                  <input type="range" min="1" max="25" step="1" v-model.number="scoreMin" class="w-full"/>
                  <div class="text-xs text-slate-500 mt-1">Atual: {{ scoreMin }}</div>
                </div>
              </div>
              <input class="w-56 border rounded-xl px-3 py-2" placeholder="Filtrar por zona/conduíte…" v-model="filtroZona"/>
            </div>
          </header>
          <div class="p-4 space-y-4">
            <div class="flex flex-wrap items-center gap-2 text-xs text-slate-600">
              <span class="inline-flex items-center gap-2"><span class="w-3 h-3 rounded border bg-emerald-100 border-emerald-300"></span>1–5</span>
              <span class="inline-flex items-center gap-2"><span class="w-3 h-3 rounded border bg-yellow-100 border-yellow-300"></span>6–10</span>
              <span class="inline-flex items-center gap-2"><span class="w-3 h-3 rounded border bg-orange-100 border-orange-300"></span>11–15</span>
              <span class="inline-flex items-center gap-2"><span class="w-3 h-3 rounded border bg-red-100 border-red-300"></span>16–25</span>
              <span class="inline-flex items-center gap-2 ml-4"><Shield class="w-3 h-3"/>score = probabilidade × impacto</span>
            </div>

            <div class="overflow-auto">
              <div class="min-w-[640px] grid grid-cols-6 gap-2">
                <div></div>
                <div v-for="p in [1,2,3,4,5]" :key="'ph'+p" class="text-center text-xs text-slate-500">Prob {{ p }}</div>

                <template v-for="i in [5,4,3,2,1]" :key="'row'+i">
                  <div class="flex items-center text-xs text-slate-500">Impacto {{ i }}</div>
                  <div v-for="p in [1,2,3,4,5]" :key="'c'+i+'-'+p" :class="['p-3 rounded-lg border transition-colors', corPorScore(i*p)]">
                    <div class="text-sm font-medium">{{ matriz[i-1][p-1].items.length }}</div>
                    <div class="text-[10px] text-slate-600">{{ i * p }}</div>
                  </div>
                </template>
              </div>
            </div>

            <div class="grid md:grid-cols-2 gap-3">
              <div v-for="r in riscosFiltrados" :key="r.id" class="p-3 rounded-xl border bg-white flex items-start gap-3">
                <AlertTriangle class="w-4 h-4 mt-0.5 text-amber-600"/>
                <div class="text-sm">
                  <div class="font-medium text-slate-800">{{ r.titulo }}</div>
                  <div class="text-xs text-slate-500">Zona: {{ r.zona }} • Prob: {{ r.prob }} • Impacto: {{ r.impacto }} • Score: {{ r.prob * r.impacto }}</div>
                </div>
              </div>
              <div v-if="riscosFiltrados.length===0" class="text-sm text-slate-500">Nenhum risco com o filtro atual.</div>
            </div>
          </div>
        </article>
      </section>

      <!-- EXPANDIR QUANDO NECESSÁRIO + PRINCÍPIOS -->
      <section class="pb-6">
        <div class="grid lg:grid-cols-3 gap-6">
          <article class="rounded-2xl shadow-sm border bg-white lg:col-span-2">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><ArrowRight class="w-4 h-4"/> Expandir quando necessário</h3>
            </header>
            <div class="p-4 space-y-3">
              <details class="rounded-lg border p-3">
                <summary class="cursor-pointer">Mapa conceitual (visão geral → detalhes)</summary>
                <div class="grid md:grid-cols-3 gap-3 text-sm mt-3">
                  <div class="p-3 rounded-lg bg-slate-50">Políticas & Papéis</div>
                  <div class="p-3 rounded-lg bg-slate-50">Zonas & Conduítes</div>
                  <div class="p-3 rounded-lg bg-slate-50">Requisitos & Controles</div>
                </div>
              </details>

              <details class="rounded-lg border p-3">
                <summary class="cursor-pointer">Glossário essencial (10 termos)</summary>
                <ul class="text-sm list-disc ml-5 space-y-1 mt-3">
                  <li>IACS: Sistemas Industriais de Automação e Controle.</li>
                  <li>CRS: Conjunto de Requisitos de Segurança por zona.</li>
                  <li>DMZ industrial: camada de separação entre TI e TO.</li>
                </ul>
              </details>

              <details class="rounded-lg border p-3">
                <summary class="cursor-pointer">Referências rápidas</summary>
                <div class="text-sm text-slate-600 mt-3">Links para normas, playbooks e evidências (ex.: 62443-2-1, 3-3, 4-2).</div>
              </details>
            </div>
          </article>

          <article class="rounded-2xl shadow-sm border bg-white">
            <header class="p-4 border-b">
              <h3 class="text-base flex items-center gap-2"><Sparkles class="w-4 h-4"/> Princípios do Padrão</h3>
            </header>
            <div class="p-4 space-y-2">
              <div v-for="(d,i) in dicas" :key="i" class="p-3 rounded-xl border bg-white">
                <div class="text-sm font-medium">{{ d.title }}</div>
                <div class="text-xs text-slate-600 mt-1">{{ d.body }}</div>
              </div>
            </div>
          </article>
        </div>
      </section>

      <!-- FOOTER -->
      <footer class="pt-6 border-t bg-white/60 rounded-xl">
        <div class="py-6 text-sm text-slate-500 flex flex-col md:flex-row items-center justify-between gap-3">
          <div>© 2035 — Padrão de Informação Otimizada</div>
          <div class="flex items-center gap-2">
            <span class="inline-flex items-center gap-1"><Sparkles class="w-4 h-4"/>IA Contextual</span>
            <span class="inline-flex items-center gap-1"><Brain class="w-4 h-4"/>Design Cognitivo</span>
            <span class="inline-flex items-center gap-1"><Focus class="w-4 h-4"/>Curadoria Contínua</span>
          </div>
        </div>
      </footer>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { AlertTriangle, ArrowRight, BookOpen, Bot, Brain, Check, Clock, Focus, Play, Search, Shield, Sparkles, Wand2, BarChart4 } from 'lucide-vue-next'

// ---------- Tipos ----------
interface Passo { id: number; texto: string; impacto: 'alto' | 'médio' | 'baixo' }
interface Risco { id: number; titulo: string; zona: string; prob: number; impacto: number }

// ---------- Mock data ----------
const resumo30s = `Segurança cibernética industrial eficaz começa com gestão (políticas, processos, pessoas) e só depois vai para controles técnicos. O sistema adapta conteúdo por perfil, contexto e objetivo — reduz carga cognitiva, prioriza riscos e gera ação.`
const microHistoria = {
  titulo: 'Por que começamos pela gestão?',
  narrativa:
    'Em 2017, uma planta similar sofreu uma parada de 18h por falha de segmentação. Um checklist de gestão teria evitado 3 decisões ruins. Resultado: prejuízo de US$ 1,2M.'
}
const passosAcao: Passo[] = [
  { id: 1, texto: 'Definir política e papéis (ISA/IEC 62443-2-1)', impacto: 'alto' },
  { id: 2, texto: 'Mapear zonas e conduítes', impacto: 'alto' },
  { id: 3, texto: 'Priorizar riscos e estabelecer metas', impacto: 'médio' },
  { id: 4, texto: 'Especificar requisitos (CRS) por zona', impacto: 'alto' },
  { id: 5, texto: 'Implantar controles e instrumentar monitoramento', impacto: 'alto' }
]
const dicas = [
  { title: 'Contexto primeiro', body: 'Mostre só o que o usuário precisa agora; o resto fica a um clique.' },
  { title: 'Chunking inteligente', body: 'Quebre conteúdo em blocos curtos conectados logicamente.' },
  { title: 'Narrativas', body: 'Explique o porquê com micro-histórias que unem dado e decisão.' },
  { title: 'Multimodal', body: 'Combine texto, voz, visual e simulação simples.' },
  { title: 'Curadoria contínua', body: 'Evite acúmulo. Consolide e remova redundâncias.' }
]
const riscos: Risco[] = [
  { id: 1, titulo: 'Acesso remoto sem MFA', zona: 'DMZ', prob: 4, impacto: 4 },
  { id: 2, titulo: 'Firmware desatualizado PLC', zona: 'Zona 1', prob: 3, impacto: 5 },
  { id: 3, titulo: 'Conduíte sem inspeção', zona: 'Conduíte A', prob: 2, impacto: 4 },
  { id: 4, titulo: 'Backups não testados', zona: 'Zona 2', prob: 3, impacto: 3 },
  { id: 5, titulo: 'Credenciais compartilhadas', zona: 'Zona 1', prob: 5, impacto: 3 },
  { id: 6, titulo: 'Segmentação insuficiente', zona: 'Zona 2', prob: 2, impacto: 5 },
  { id: 7, titulo: 'Estação de engenharia exposta', zona: 'DMZ', prob: 3, impacto: 4 }
]

// ---------- Estado ----------
const densidade = ref<number>(60)
const modoProfundo = ref(false)
const itensConcluidos = ref<number[]>([])
const filtro = ref('')
const filtroZona = ref('')
const scoreMin = ref<number>(9)
const pergunta = ref('')
const aba = ref<'acao'|'aprendizado'|'auditoria'>('acao')

// ---------- Computeds ----------
const passosFiltrados = computed(() =>
  passosAcao.filter(p => p.texto.toLowerCase().includes(filtro.value.toLowerCase()))
)
const riscosFiltrados = computed(() =>
  riscos.filter(r => (filtroZona.value ? r.zona.toLowerCase().includes(filtroZona.value.toLowerCase()) : true) && (r.prob * r.impacto >= scoreMin.value))
)
const matriz = computed(() => {
  const grid: { items: Risco[] }[][] = Array.from({ length: 5 }, () => Array.from({ length: 5 }, () => ({ items: [] as Risco[] })))
  riscosFiltrados.value.forEach(r => {
    const p = Math.min(Math.max(r.prob, 1), 5)
    const i = Math.min(Math.max(r.impacto, 1), 5)
    grid[i - 1][p - 1].items.push(r)
  })
  return grid
})

// ---------- Métodos ----------
function corPorScore(score: number) {
  if (score >= 16) return 'bg-red-100 border-red-300'
  if (score >= 11) return 'bg-orange-100 border-orange-300'
  if (score >= 6) return 'bg-yellow-100 border-yellow-300'
  return 'bg-emerald-100 border-emerald-300'
}
function alternarChecklist(id: number) {
  const i = itensConcluidos.value.indexOf(id)
  if (i >= 0) itensConcluidos.value.splice(i, 1)
  else itensConcluidos.value.push(id)
}

// Dialog state
const dialogAberto = ref(false)

// Classes Tabs
const abaOn = 'text-slate-900 bg-slate-100 px-3 py-1.5 text-sm'
const abaOff = 'text-slate-600 hover:text-slate-900 px-3 py-1.5 text-sm'
</script>

<style scoped>
.fade-enter-active, .fade-leave-active { transition: opacity .15s ease }
.fade-enter-from, .fade-leave-to { opacity: 0 }
.list-enter-active, .list-leave-active { transition: all .2s ease }
.list-enter-from { opacity: 0; transform: translateY(6px) }
.list-leave-to { opacity: 0; transform: translateY(-6px) }
</style>
