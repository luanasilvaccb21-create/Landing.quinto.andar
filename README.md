import React, { useMemo, useState } from "react";
import { motion } from "framer-motion";
import { Check, ChevronRight, Phone, Mail, MessageSquare, Home, Building2, ShieldCheck, Clock, MapPin, Sparkles, Star, ArrowUpRight, ClipboardList, Send } from "lucide-react";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";

/**
 * Landing de captação inspirada no estilo do QuintoAndar (paleta azul + branco, tipografia arredondada)
 * - Estrutura de seções: Hero, Destaques (Alugar / Vender), Sobre a corretora, Depoimentos, FAQ, Formulário, Footer
 * - CTAs: WhatsApp, E‑mail e telefone
 * - Formulário de interesse com opção Alugar ou Vender
 * - Botão flutuante do WhatsApp
 * - Animações com Framer Motion
 *
 * Como usar:
 * 1) Atualize os dados de contato (whatsNumber, emailDestino, creci, nomeCorretora).
 * 2) Publique em qualquer ambiente React (Vite, Next, CRA) — Tailwind + shadcn/ui já disponíveis no playground.
 */

export default function LandingCaptacao() {
  // ====== CONFIGURAÇÕES RÁPIDAS ======
  const nomeCorretora = "Sua Tia – Corretora";
  const creci = "CRECI 000000";
  const whatsNumber = "+55 11 90000-0000"; // Ex.: +55 11 91234-5678
  const emailDestino = "contato@sua-corretora.com";
  const telefoneDireto = "(11) 0000-0000";

  // links montados para CTA
  const whatsHref = useMemo(() => `https://wa.me/55${whatsNumber.replace(/\D/g, "")}?text=${encodeURIComponent(
    "Olá! Tenho interesse em imóveis (alugar/vender)."
  )}`, [whatsNumber]);
  const mailHref = `mailto:${emailDestino}?subject=${encodeURIComponent("Quero falar sobre imóveis")}`;
  const phoneHref = `tel:${telefoneDireto.replace(/\D/g, "")}`;

  // ====== ESTADO DO FORMULÁRIO ======
  const [tipoInteresse, setTipoInteresse] = useState<"alugar" | "vender" | "indefinido">("indefinido");
  const [nome, setNome] = useState("");
  const [email, setEmail] = useState("");
  const [telefone, setTelefone] = useState("");
  const [bairro, setBairro] = useState("");
  const [mensagem, setMensagem] = useState("");

  const handleEnviar = (e: React.FormEvent) => {
    e.preventDefault();
    const assunto = `Contato – Interesse em ${tipoInteresse !== "indefinido" ? tipoInteresse : "imóveis"}`;
    const corpo = [
      `Nome: ${nome}`,
      `E‑mail: ${email}`,
      `Telefone: ${telefone}`,
      `Bairro/Cidade: ${bairro}`,
      `Interesse: ${tipoInteresse}`,
      "Mensagem:",
      mensagem || "(sem mensagem)",
    ].join("%0D%0A");

    // abre e-mail já preenchido; alternativa: enviar para WhatsApp
    const mailto = `mailto:${emailDestino}?subject=${encodeURIComponent(assunto)}&body=${corpo}`;
    window.location.href = mailto;
  };

  // ====== ESTILOS GERAIS ======
  // Paleta: azul principal, azuis claros, branco
  const azul = "#2563eb"; // azul vibrante (aprox.)
  const azulEscuro = "#1e40af";
  const azulClaro = "#dbeafe";

  const container = "max-w-7xl mx-auto px-4 sm:px-6 lg:px-8";
  const section = "py-16 md:py-20";

  // Variants animação
  const fadeUp = {
    initial: { opacity: 0, y: 24 },
    whileInView: { opacity: 1, y: 0 },
    viewport: { once: true, amount: 0.2 },
    transition: { duration: 0.6, ease: "easeOut" },
  } as const;

  return (
    <div className="font-sans text-slate-800" style={{
      // tipografia levemente arredondada
      fontFamily: "ui-rounded, system-ui, -apple-system, Segoe UI, Roboto, 'Helvetica Neue', 'Noto Sans', Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', Arial, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'",
    }}>
      {/* ====== HERO ====== */}
      <header className="relative overflow-hidden" style={{ background: `linear-gradient(135deg, ${azul} 0%, ${azulEscuro} 100%)` }}>
        <div className={`${container} ${section} relative z-10`}>          
          <motion.div {...fadeUp} className="text-white max-w-3xl">
            <span className="inline-flex items-center gap-2 rounded-full bg-white/10 px-3 py-1 text-sm backdrop-blur-md ring-1 ring-white/20 mb-4">
              <Sparkles className="h-4 w-4" /> Atendimento digital, rápido e seguro
            </span>
            <h1 className="text-3xl md:text-5xl font-extrabold leading-tight tracking-tight">
              Alugue ou venda seu imóvel <span className="inline-block">sem burocracia</span>
            </h1>
            <p className="mt-4 text-lg md:text-xl text-white/90">
              Plataforma moderna com contrato digital, divulgação profissional e acompanhamento completo. Tudo online, no seu tempo.
            </p>
            <div className="mt-8 flex flex-wrap items-center gap-3">
              <Button size="lg" className="rounded-2xl text-base px-6 py-6 bg-white text-slate-900 hover:bg-white/90" asChild>
                <a href="#formulario"><ClipboardList className="h-5 w-5 mr-2"/>Quero falar agora</a>
              </Button>
              <Button size="lg" variant="secondary" className="rounded-2xl text-base px-6 py-6 bg-transparent border border-white/30 text-white hover:bg-white/10" asChild>
                <a href="#alugar"><Home className="h-5 w-5 mr-2"/>Quero Alugar</a>
              </Button>
              <Button size="lg" variant="secondary" className="rounded-2xl text-base px-6 py-6 bg-transparent border border-white/30 text-white hover:bg-white/10" asChild>
                <a href="#vender"><Building2 className="h-5 w-5 mr-2"/>Quero Vender</a>
              </Button>
            </div>
            <div className="mt-6 flex flex-wrap items-center gap-6 text-white/80 text-sm">
              <div className="inline-flex items-center gap-2"><ShieldCheck className="h-4 w-4"/> Contrato digital seguro</div>
              <div className="inline-flex items-center gap-2"><Clock className="h-4 w-4"/> Agendamento online</div>
              <div className="inline-flex items-center gap-2"><MapPin className="h-4 w-4"/> Atuação local</div>
            </div>
          </motion.div>
        </div>

        {/* fundo decorativo */}
        <div className="absolute inset-0 -z-0 opacity-20 pointer-events-none" aria-hidden>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 600" className="w-full h-full">
            <defs>
              <radialGradient id="g" cx="50%" cy="50%" r="60%">
                <stop offset="0%" stopColor="#ffffff" stopOpacity="0.7"/>
                <stop offset="100%" stopColor="#ffffff" stopOpacity="0"/>
              </radialGradient>
            </defs>
            <rect width="800" height="600" fill="url(#g)"/>
          </svg>
        </div>
      </header>

      {/* ====== SEÇÃO: ALUGAR ====== */}
      <section id="alugar" className={`${section} bg-white`}>
        <div className={container}>
          <motion.div {...fadeUp} className="mb-10">
            <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Aluguel sem complicação</h2>
            <p className="mt-3 text-slate-600 max-w-2xl">Sem fiador, sem caução e com assinatura 100% digital. Vistoria detalhada e pagamento garantido ao proprietário.</p>
          </motion.div>

          <div className="grid md:grid-cols-3 gap-6">
            {[
              { icon: <ShieldCheck className="h-5 w-5"/>, title: "Sem fiador e sem caução", desc: "Aprovação simplificada para você entrar logo no imóvel." },
              { icon: <Clock className="h-5 w-5"/>, title: "Processo 100% online", desc: "Da visita ao contrato, tudo feito de forma digital e prática." },
              { icon: <Check className="h-5 w-5"/>, title: "Vistoria e segurança", desc: "Registro do estado do imóvel na entrada e saída." },
            ].map((f, i) => (
              <motion.div key={i} {...fadeUp} transition={{ ...fadeUp.transition, delay: 0.05 * i }}>
                <Card className="rounded-2xl shadow-sm hover:shadow-md transition-shadow">
                  <CardHeader>
                    <CardTitle className="flex items-center gap-2 text-base">{f.icon} {f.title}</CardTitle>
                  </CardHeader>
                  <CardContent className="text-slate-600">{f.desc}</CardContent>
                </Card>
              </motion.div>
            ))}
          </div>

          <div className="mt-8">
            <Button className="rounded-2xl px-6 py-6 text-base bg-slate-900 hover:bg-slate-800" asChild>
              <a href="#formulario"><ChevronRight className="h-5 w-5 mr-2"/>Tenho interesse em alugar</a>
            </Button>
          </div>
        </div>
      </section>

      {/* ====== SEÇÃO: VENDER ====== */}
      <section id="vender" className={`${section}`} style={{ background: azulClaro }}>
        <div className={container}>
          <motion.div {...fadeUp} className="mb-10">
            <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Venda com praticidade e alcance</h2>
            <p className="mt-3 text-slate-700 max-w-2xl">Anuncie sem custo inicial, receba propostas qualificadas e tenha apoio na negociação até a assinatura.</p>
          </motion.div>

          <div className="grid md:grid-cols-3 gap-6">
            {[
              { icon: <Sparkles className="h-5 w-5"/>, title: "Anúncio profissional", desc: "Divulgação ampla para alcançar mais compradores." },
              { icon: <Star className="h-5 w-5"/>, title: "Avaliação justa", desc: "Preço alinhado ao mercado para vender mais rápido." },
              { icon: <ShieldCheck className="h-5 w-5"/>, title: "Suporte jurídico", desc: "Acompanhamento seguro da proposta à escritura." },
            ].map((f, i) => (
              <motion.div key={i} {...fadeUp} transition={{ ...fadeUp.transition, delay: 0.05 * i }}>
                <Card className="rounded-2xl shadow-sm hover:shadow-md transition-shadow">
                  <CardHeader>
                    <CardTitle className="flex items-center gap-2 text-base">{f.icon} {f.title}</CardTitle>
                  </CardHeader>
                  <CardContent className="text-slate-600">{f.desc}</CardContent>
                </Card>
              </motion.div>
            ))}
          </div>

          <div className="mt-8">
            <Button className="rounded-2xl px-6 py-6 text-base" style={{ backgroundColor: azul, color: "white" }} asChild>
              <a href="#formulario"><ChevronRight className="h-5 w-5 mr-2"/>Tenho interesse em vender</a>
            </Button>
          </div>
        </div>
      </section>

      {/* ====== SOBRE A CORRETORA ====== */}
      <section id="sobre" className={`${section} bg-white`}>
        <div className={container}>
          <motion.div {...fadeUp} className="grid md:grid-cols-2 gap-10 items-center">
            <div>
              <h2 className="text-2xl md:text-4xl font-bold tracking-tight">{nomeCorretora}</h2>
              <p className="mt-3 text-slate-600">Atendimento humano com a eficiência do digital. Orientação completa para você alugar ou vender com segurança e rapidez.</p>
              <ul className="mt-6 space-y-3 text-slate-700">
                {[
                  "Atuação em bairros-chave da cidade",
                  "Visitas e propostas com agendamento online",
                  "Transparência em cada etapa do processo",
                ].map((t, i) => (
                  <li key={i} className="flex items-start gap-3"><Check className="h-5 w-5 mt-0.5 text-emerald-600"/><span>{t}</span></li>
                ))}
              </ul>
              <div className="mt-6 text-sm text-slate-500">{creci}</div>
              <div className="mt-6 flex flex-wrap gap-3">
                <Button className="rounded-2xl" asChild>
                  <a href={whatsHref} target="_blank" rel="noreferrer"><MessageSquare className="h-4 w-4 mr-2"/>WhatsApp</a>
                </Button>
                <Button variant="outline" className="rounded-2xl" asChild>
                  <a href={mailHref}><Mail className="h-4 w-4 mr-2"/>E‑mail</a>
                </Button>
                <Button variant="outline" className="rounded-2xl" asChild>
                  <a href={phoneHref}><Phone className="h-4 w-4 mr-2"/>Telefone</a>
                </Button>
              </div>
            </div>
            <div>
              <Card className="rounded-2xl overflow-hidden">
                <CardContent className="p-0">
                  <img src="https://images.unsplash.com/photo-1501183638710-841dd1904471?q=80&w=1640&auto=format&fit=crop" alt="Foto de imóvel moderno" className="w-full h-[320px] object-cover"/>
                </CardContent>
              </Card>
            </div>
          </motion.div>
        </div>
      </section>

      {/* ====== DEPOIMENTOS ====== */}
      <section className={`${section}`} style={{ background: azulClaro }}>
        <div className={container}>
          <motion.div {...fadeUp} className="mb-8">
            <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Quem já fez, recomenda</h2>
            <p className="mt-3 text-slate-700">Histórias reais de quem alugou ou vendeu rápido e sem dor de cabeça.</p>
          </motion.div>
          <div className="grid md:grid-cols-3 gap-6">
            {[
              {
                nome: "Marina S.",
                texto: "Aluguei em menos de 10 dias. Tudo digital e super organizado!",
              },
              {
                nome: "Carlos A.",
                texto: "Vendi meu apê com avaliação justa e acompanhamento em cada etapa.",
              },
              {
                nome: "Patrícia R.",
                texto: "Sem fiador e com vistoria detalhada, me senti segura do início ao fim.",
              },
            ].map((d, i) => (
              <motion.div key={i} {...fadeUp} transition={{ ...fadeUp.transition, delay: 0.05 * i }}>
                <Card className="rounded-2xl shadow-sm h-full">
                  <CardContent className="pt-6">
                    <div className="flex items-center gap-1 mb-3" aria-label="Avaliação 5 estrelas">
                      {[...Array(5)].map((_, j) => <Star key={j} className="h-4 w-4" />)}
                    </div>
                    <p className="text-slate-700">“{d.texto}”</p>
                    <div className="mt-4 text-sm text-slate-500">{d.nome}</div>
                  </CardContent>
                </Card>
              </motion.div>
            ))}
          </div>
        </div>
      </section>

      {/* ====== FAQ ====== */}
      <section className={`${section} bg-white`}>
        <div className={container}>
          <motion.div {...fadeUp} className="mb-8">
            <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Perguntas frequentes</h2>
            <p className="mt-3 text-slate-600">Algumas dúvidas comuns sobre aluguel e venda.</p>
          </motion.div>
          <div className="grid md:grid-cols-2 gap-6">
            {[
              { q: "Preciso de fiador para alugar?", a: "Não. A aprovação é simplificada e o contrato é 100% digital." },
              { q: "Como funciona a avaliação para venda?", a: "Analisamos o mercado local para precificar de forma justa e estratégica." },
              { q: "Posso agendar visitas online?", a: "Sim, fazemos o agendamento de forma digital e prática." },
              { q: "Existe taxa para anunciar?", a: "O anúncio inicial pode ser gratuito; taxas e condições variam por serviço contratado." },
            ].map((f, i) => (
              <Card key={i} className="rounded-2xl shadow-sm">
                <CardHeader>
                  <CardTitle className="text-base">{f.q}</CardTitle>
                </CardHeader>
                <CardContent className="text-slate-600">{f.a}</CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* ====== FORMULÁRIO ====== */}
      <section id="formulario" className={`${section}`} style={{ background: azulClaro }}>
        <div className={container}>
          <motion.div {...fadeUp} className="mb-8 text-center max-w-3xl mx-auto">
            <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Fale com a corretora</h2>
            <p className="mt-3 text-slate-700">Preencha seus dados e selecione seu objetivo. Entraremos em contato ainda hoje.</p>
          </motion.div>

          <Card className="rounded-2xl max-w-3xl mx-auto">
            <CardContent className="p-6 md:p-8">
              <form onSubmit={handleEnviar} className="grid gap-4">
                <div className="grid grid-cols-1 md:grid-cols-3 gap-3">
                  <Button type="button" variant={tipoInteresse === "alugar" ? "default" : "outline"} className="rounded-2xl" onClick={() => setTipoInteresse("alugar")}>Quero alugar</Button>
                  <Button type="button" variant={tipoInteresse === "vender" ? "default" : "outline"} className="rounded-2xl" onClick={() => setTipoInteresse("vender")}>Quero vender</Button>
                  <Button type="button" variant={tipoInteresse === "indefinido" ? "default" : "outline"} className="rounded-2xl" onClick={() => setTipoInteresse("indefinido")}>Ainda avaliando</Button>
                </div>

                <div className="grid md:grid-cols-2 gap-4">
                  <div>
                    <label className="text-sm text-slate-600">Nome</label>
                    <Input required placeholder="Seu nome" value={nome} onChange={(e) => setNome(e.target.value)} className="rounded-2xl"/>
                  </div>
                  <div>
                    <label className="text-sm text-slate-600">E‑mail</label>
                    <Input type="email" required placeholder="seu@email.com" value={email} onChange={(e) => setEmail(e.target.value)} className="rounded-2xl"/>
                  </div>
                </div>

                <div className="grid md:grid-cols-2 gap-4">
                  <div>
                    <label className="text-sm text-slate-600">Telefone / WhatsApp</label>
                    <Input required placeholder="(11) 9 0000-0000" value={telefone} onChange={(e) => setTelefone(e.target.value)} className="rounded-2xl"/>
                  </div>
                  <div>
                    <label className="text-sm text-slate-600">Bairro / Cidade</label>
                    <Input placeholder="Ex.: Santo Amaro, São Paulo" value={bairro} onChange={(e) => setBairro(e.target.value)} className="rounded-2xl"/>
                  </div>
                </div>

                <div>
                  <label className="text-sm text-slate-600">Mensagem</label>
                  <Textarea placeholder="Conte um pouco do que você procura ou do seu imóvel" value={mensagem} onChange={(e) => setMensagem(e.target.value)} className="rounded-2xl min-h-[100px]"/>
                </div>

                <div className="flex flex-wrap gap-3 items-center">
                  <Button type="submit" className="rounded-2xl"><Send className="h-4 w-4 mr-2"/>Enviar</Button>
                  <Button type="button" variant="outline" className="rounded-2xl" asChild>
                    <a href={whatsHref} target="_blank" rel="noreferrer"><MessageSquare className="h-4 w-4 mr-2"/>Chamar no WhatsApp</a>
                  </Button>
                </div>

                <p className="text-xs text-slate-500">Ao enviar, abrimos o e‑mail com seus dados preenchidos. Você pode também falar direto pelo WhatsApp.</p>
              </form>
            </CardContent>
          </Card>
        </div>
      </section>

      {/* ====== RODAPÉ ====== */}
      <footer className="py-10" style={{ background: azulEscuro }}>
        <div className={`${container} flex flex-col md:flex-row items-center justify-between gap-4`}>
          <div className="text-white/90 text-sm">
            <div className="font-semibold">{nomeCorretora}</div>
            <div className="opacity-80">{creci}</div>
          </div>
          <div className="flex flex-wrap gap-3">
            <Button size="sm" className="rounded-xl" asChild>
              <a href={whatsHref} target="_blank" rel="noreferrer"><MessageSquare className="h-4 w-4 mr-2"/>WhatsApp</a>
            </Button>
            <Button size="sm" variant="secondary" className="rounded-xl" asChild>
              <a href={mailHref}><Mail className="h-4 w-4 mr-2"/>E‑mail</a>
            </Button>
            <Button size="sm" variant="secondary" className="rounded-xl" asChild>
              <a href={phoneHref}><Phone className="h-4 w-4 mr-2"/>Telefone</a>
            </Button>
          </div>
        </div>
      </footer>

      {/* ====== BOTÃO FLUTUANTE WHATSAPP ====== */}
      <a href={whatsHref} target="_blank" rel="noreferrer" className="fixed bottom-5 right-5 inline-flex items-center justify-center w-14 h-14 rounded-full shadow-lg ring-1 ring-black/5" style={{ backgroundColor: "#25D366", color: "white" }} aria-label="Abrir WhatsApp">
        <MessageSquare className="h-7 w-7"/>
      </a>

      {/* ====== VOLTAR AO TOPO ====== */}
      <a href="#" className="fixed bottom-5 left-5 inline-flex items-center gap-1 text-sm px-3 py-2 rounded-full bg-white shadow ring-1 ring-black/5 text-slate-700 hover:bg-slate-50">
        Topo <ArrowUpRight className="h-4 w-4"/>
      </a>
    </div>
  );
}
