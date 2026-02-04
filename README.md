# ID-CORP
import React, { useState, useEffect } from 'react';
import { 
  Lock, 
  User, 
  Users, 
  TrendingUp, 
  Zap, 
  Coins, 
  Gift, 
  Map, 
  Mail, 
  ChevronRight, 
  LogOut, 
  CheckCircle2,
  Building2,
  Trophy,
  Search,
  Utensils
} from 'lucide-react';

const App = () => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  const [user, setUser] = useState(null);
  const [activeTab, setActiveTab] = useState('dashboard');
  const [coins, setCoins] = useState(1250);
  const [notifications, setNotifications] = useState(1);

  // Credenciales preestablecidas
  const [email, setEmail] = useState('admin@idcorp.com');
  const [password, setPassword] = useState('idcorp2024');

  const handleLogin = (e) => {
    e.preventDefault();
    setIsAuthenticated(true);
    setUser({ name: "Alex I+D", role: "Investigador Senior", dept: "Biotecnología" });
  };

  if (!isAuthenticated) {
    return (
      <div className="min-h-screen bg-slate-950 flex items-center justify-center p-4">
        <div className="max-w-md w-full bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8 shadow-2xl">
          <div className="text-center mb-8">
            <div className="bg-indigo-600/20 w-16 h-16 rounded-2xl flex items-center justify-center mx-auto mb-4 border border-indigo-500/30">
              <Lock className="text-indigo-400" size={32} />
            </div>
            <h1 className="text-2xl font-black text-white italic uppercase tracking-tighter">Acceso I+D Corp</h1>
            <p className="text-slate-400 text-sm">Credenciales de acceso rápido preestablecidas</p>
          </div>
          <form onSubmit={handleLogin} className="space-y-4">
            <div>
              <label className="text-xs font-bold text-slate-500 uppercase ml-2">Email Corporativo</label>
              <input 
                type="email" 
                required 
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white focus:ring-2 focus:ring-indigo-500 outline-none transition-all" 
                placeholder="usuario@idcorp.com" 
              />
            </div>
            <div>
              <label className="text-xs font-bold text-slate-500 uppercase ml-2">Contraseña</label>
              <input 
                type="password" 
                required 
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white focus:ring-2 focus:ring-indigo-500 outline-none transition-all" 
                placeholder="••••••••" 
              />
            </div>
            <button className="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-black py-4 rounded-2xl shadow-lg shadow-indigo-500/20 transition-all flex items-center justify-center gap-2 uppercase tracking-widest text-sm">
              Entrar al Ecosistema <ChevronRight size={18} />
            </button>
          </form>
          <div className="mt-6 p-4 bg-indigo-500/5 rounded-2xl border border-indigo-500/10">
            <p className="text-center text-slate-500 text-[10px] uppercase font-bold tracking-widest">
              Usa el botón superior para entrar directamente con las claves de demo.
            </p>
          </div>
        </div>
      </div>
    );
  }

  const SidebarItem = ({ id, icon: Icon, label }) => (
    <button 
      onClick={() => setActiveTab(id)}
      className={`w-full flex items-center gap-3 px-4 py-4 rounded-2xl font-bold text-sm transition-all mb-2 ${activeTab === id ? 'bg-indigo-600 text-white shadow-lg' : 'text-slate-400 hover:bg-slate-800'}`}
    >
      <Icon size={20} />
      <span className="hidden md:inline">{label}</span>
    </button>
  );

  return (
    <div className="min-h-screen bg-slate-950 text-slate-200 flex">
      <aside className="w-20 md:w-64 bg-slate-900 border-r border-slate-800 p-4 flex flex-col">
        <div className="mb-10 text-center md:text-left px-2">
          <h2 className="text-indigo-400 font-black italic text-xl">I+D HUB</h2>
        </div>
        <nav className="flex-grow">
          <SidebarItem id="dashboard" icon={Map} label="Dashboard" />
          <SidebarItem id="contrato" icon={TrendingUp} label="Contrato 3D" />
          <SidebarItem id="misiones" icon={Zap} label="Misiones Pro" />
          <SidebarItem id="micropolix" icon={Building2} label="Micropolix" />
          <SidebarItem id="bonos" icon={Gift} label="Bonificaciones" />
        </nav>
        <div className="mt-auto p-2">
          <div className="bg-amber-500/10 border border-amber-500/20 rounded-2xl p-3 flex items-center gap-3 mb-4">
            <Coins className="text-amber-500" size={20} />
            <span className="font-black text-amber-500 text-lg hidden md:inline">{coins}</span>
          </div>
          <button onClick={() => setIsAuthenticated(false)} className="w-full flex items-center gap-3 px-4 py-3 text-rose-500 font-bold hover:bg-rose-500/10 rounded-xl transition-all">
            <LogOut size={20} />
            <span className="hidden md:inline text-xs uppercase tracking-widest">Salir</span>
          </button>
        </div>
      </aside>

      <main className="flex-grow p-6 md:p-10 overflow-y-auto">
        <header className="flex justify-between items-center mb-10">
          <div>
            <h1 className="text-3xl font-black text-white italic uppercase tracking-tighter">
              {activeTab === 'dashboard' && 'Ecosistema de Impacto'}
              {activeTab === 'contrato' && 'Dimensión 1: Contrato 3D'}
              {activeTab === 'misiones' && 'Dimensión 2: Misiones Pro'}
              {activeTab === 'micropolix' && 'Dimensión 3: Micropolix'}
              {activeTab === 'bonos' && 'Bonus Marketplace'}
            </h1>
            <p className="text-slate-400 text-sm">{user.name} • {user.dept}</p>
          </div>
          <div className="flex items-center gap-4">
            <div className="relative cursor-pointer">
              <Mail className="text-slate-400" />
              {notifications > 0 && <span className="absolute -top-1 -right-1 bg-rose-500 w-4 h-4 rounded-full text-[10px] flex items-center justify-center font-bold">1</span>}
            </div>
          </div>
        </header>

        {activeTab === 'dashboard' && <DashboardView coins={coins} setActiveTab={setActiveTab} />}
        {activeTab === 'contrato' && <Contrato3DView setCoins={setCoins} />}
        {activeTab === 'misiones' && <MisionesProView setCoins={setCoins} />}
        {activeTab === 'micropolix' && <MicropolixView />}
        {activeTab === 'bonos' && <BonosView coins={coins} setCoins={setCoins} />}
      </main>
    </div>
  );
};

const DashboardView = ({ coins, setActiveTab }) => (
  <div className="grid md:grid-cols-3 gap-6">
    <div className="md:col-span-2 space-y-6">
      <div className="bg-gradient-to-br from-indigo-600 to-purple-700 rounded-[2.5rem] p-8 shadow-xl text-white relative overflow-hidden">
        <div className="relative z-10">
          <h2 className="text-3xl font-black italic uppercase mb-2">¡Bienvenido de nuevo, Alex!</h2>
          <p className="text-indigo-100 max-w-md">Tu impacto cultural este mes ha subido un 12%. Tienes nuevas misiones disponibles fuera de tu área.</p>
          <button onClick={() => setActiveTab('misiones')} className="mt-6 bg-white text-indigo-600 px-6 py-3 rounded-xl font-black text-sm uppercase tracking-widest hover:bg-slate-100 transition-all">Ver Misiones</button>
        </div>
        <Zap className="absolute right-[-20px] bottom-[-20px] text-white/10 w-64 h-64 rotate-12" />
      </div>
      <div className="grid grid-cols-2 gap-6">
        <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6">
          <div className="flex justify-between items-center mb-4">
            <h4 className="text-slate-400 font-bold uppercase text-xs">Progreso Trimestral</h4>
            <Trophy className="text-amber-500" size={18} />
          </div>
          <div className="flex items-end gap-2">
            <span className="text-4xl font-black text-white">84%</span>
            <span className="text-emerald-400 font-bold text-xs mb-1">+5%</span>
          </div>
        </div>
        <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6">
          <div className="flex justify-between items-center mb-4">
            <h4 className="text-slate-400 font-bold uppercase text-xs">Bio-Credits</h4>
            <Coins className="text-amber-500" size={18} />
          </div>
          <div className="flex items-end gap-2">
            <span className="text-4xl font-black text-white">{coins}</span>
            <span className="text-slate-500 font-bold text-xs mb-1">Total</span>
          </div>
        </div>
      </div>
    </div>
    <div className="bg-slate-900 border border-slate-800 rounded-[2.5rem] p-6">
      <h3 className="text-lg font-black text-white italic uppercase mb-6">Última Misión</h3>
      <div className="space-y-4">
        {[1, 2, 3].map(i => (
          <div key={i} className="flex gap-4 p-3 hover:bg-slate-800 rounded-2xl transition-all cursor-pointer border border-transparent hover:border-slate-700">
            <div className="bg-slate-800 w-12 h-12 rounded-xl flex items-center justify-center shrink-0">
              <Mail className="text-indigo-400" size={20} />
            </div>
            <div>
              <p className="text-sm font-bold text-white">Misión Flash Completada</p>
              <p className="text-[10px] text-slate-500 uppercase font-black">Recompensa: +50 Monedas</p>
            </div>
          </div>
        ))}
      </div>
    </div>
  </div>
);

const Contrato3DView = ({ setCoins }) => {
  const [steps, setSteps] = useState([false, false, false]);
  
  const handleComplete = (idx) => {
    if(!steps[idx]) {
      const newSteps = [...steps];
      newSteps[idx] = true;
      setSteps(newSteps);
      setCoins(prev => prev + 200);
    }
  };

  return (
    <div className="space-y-8 animate-in fade-in slide-in-from-bottom-4">
      <div className="grid md:grid-cols-3 gap-6">
        <div className={`p-8 rounded-[2.5rem] border transition-all ${steps[0] ? 'bg-emerald-500/5 border-emerald-500/20' : 'bg-slate-900 border-slate-800'}`}>
          <User className="text-indigo-400 mb-6" size={40} />
          <h3 className="text-xl font-black text-white uppercase italic mb-2">Dimensión Personal</h3>
          <p className="text-slate-400 text-sm mb-6">¿Cómo te ves hoy en tu puesto? Define tu propósito y tus motivaciones intrínsecas.</p>
          <button onClick={() => handleComplete(0)} disabled={steps[0]} className={`w-full py-3 rounded-xl font-black text-xs uppercase tracking-widest ${steps[0] ? 'bg-emerald-500 text-white' : 'bg-indigo-600 text-white hover:bg-indigo-500'}`}>
            {steps[0] ? 'Completado +200' : 'Definir Visión'}
          </button>
        </div>
        <div className={`p-8 rounded-[2.5rem] border transition-all ${steps[1] ? 'bg-emerald-500/5 border-emerald-500/20' : 'bg-slate-900 border-slate-800'}`}>
          <Users className="text-purple-400 mb-6" size={40} />
          <h3 className="text-xl font-black text-white uppercase italic mb-2">Dimensión Colectiva</h3>
          <p className="text-slate-400 text-sm mb-6">¿Cómo te percibe el equipo? El impacto que generas en el ecosistema diario de I+D.</p>
          <button onClick={() => handleComplete(1)} disabled={steps[1]} className={`w-full py-3 rounded-xl font-black text-xs uppercase tracking-widest ${steps[1] ? 'bg-emerald-500 text-white' : 'bg-indigo-600 text-white hover:bg-indigo-500'}`}>
            {steps[1] ? 'Completado +200' : 'Recibir Feedback'}
          </button>
        </div>
        <div className={`p-8 rounded-[2.5rem] border transition-all ${steps[2] ? 'bg-emerald-500/5 border-emerald-500/20' : 'bg-slate-900 border-slate-800'}`}>
          <TrendingUp className="text-amber-400 mb-6" size={40} />
          <h3 className="text-xl font-black text-white uppercase italic mb-2">Dimensión Evolutiva</h3>
          <p className="text-slate-400 text-sm mb-6">Plan de desarrollo a 90 días. ¿Qué habilidades vas a desbloquear próximamente?</p>
          <button onClick={() => handleComplete(2)} disabled={steps[2]} className={`w-full py-3 rounded-xl font-black text-xs uppercase tracking-widest ${steps[2] ? 'bg-emerald-500 text-white' : 'bg-indigo-600 text-white hover:bg-indigo-500'}`}>
            {steps[2] ? 'Completado +200' : 'Trazar Plan'}
          </button>
        </div>
      </div>
      <div className="bg-slate-900 border border-slate-800 rounded-[2.5rem] p-8">
        <h4 className="font-black text-white italic uppercase mb-4">¿Por qué 3D?</h4>
        <p className="text-slate-400 leading-relaxed">
          En nuestra empresa de I+D, el talento no es una línea plana. Eres un profesional tridimensional. Al completar estas tres dimensiones, no solo ganas Bio-Credits, sino que alineas tu propósito personal con el éxito colectivo.
        </p>
      </div>
    </div>
  );
};

const MisionesProView = ({ setCoins }) => {
  const [mission, setMission] = useState(null);
  const [generating, setGenerating] = useState(false);

  const colleagues = ["Lucía (Finanzas)", "Marc (Legal)", "Sara (Logística)", "Hugo (Ventas)", "Elena (RRHH)"];
  const tasks = [
    "descubrir cuál es su color favorito",
    "preguntar qué es lo que más le apasiona de su puesto",
    "tomar un café virtual de 10 min y conocer su hobby secreto",
    "descubrir qué música escucha para concentrarse",
    "conocer qué hito de I+D le gustaría ver cumplido este año"
  ];

  const generateMission = () => {
    setGenerating(true);
    setTimeout(() => {
      const randomColleague = colleagues[Math.floor(Math.random() * colleagues.length)];
      const randomTask = tasks[Math.floor(Math.random() * tasks.length)];
      setMission({ colleague: randomColleague, task: randomTask });
      setGenerating(false);
    }, 1500);
  };

  return (
    <div className="max-w-2xl mx-auto space-y-8 animate-in fade-in slide-in-from-bottom-4">
      <div className="bg-slate-900 border border-slate-800 rounded-[3rem] p-10 text-center">
        <div className="bg-indigo-600/20 w-20 h-20 rounded-3xl flex items-center justify-center mx-auto mb-6">
          <Zap className="text-indigo-400" size={40} />
        </div>
        <h2 className="text-3xl font-black text-white italic uppercase mb-4">Misiones Flash</h2>
        <p className="text-slate-400 mb-8 font-medium">Recibirás una notificación en tu correo. Tu objetivo: conectar con alguien fuera de tu departamento y completar el reto para ganar Bio-Credits.</p>
        
        {mission ? (
          <div className="bg-indigo-600/10 border border-indigo-500/30 rounded-3xl p-8 mb-8 animate-in zoom-in">
            <h4 className="text-indigo-400 font-black uppercase tracking-widest text-xs mb-4">Misión Asignada</h4>
            <p className="text-xl text-white font-bold leading-relaxed">
              Tu compañero es <span className="text-indigo-400">{mission.colleague}</span>. <br/>
              Tu misión es <span className="italic">"{mission.task}"</span>.
            </p>
            <div className="mt-6 flex justify-center gap-4">
              <button onClick={() => { setCoins(p => p + 100); setMission(null); }} className="bg-emerald-500 text-white px-6 py-3 rounded-xl font-black text-xs uppercase tracking-widest">Misión Cumplida +100</button>
            </div>
          </div>
        ) : (
          <button 
            onClick={generateMission} 
            disabled={generating}
            className="bg-indigo-600 hover:bg-indigo-500 text-white px-10 py-5 rounded-3xl font-black text-lg uppercase tracking-tighter shadow-xl shadow-indigo-600/20 transition-all flex items-center gap-3 mx-auto"
          >
            {generating ? <span className="animate-pulse">Conectando...</span> : <>Generar Misión <Zap size={20}/></>}
          </button>
        )}
      </div>
    </div>
  );
};

const MicropolixView = () => {
  const [submitted, setSubmitted] = useState(false);

  return (
    <div className="max-w-3xl mx-auto animate-in fade-in slide-in-from-bottom-4">
      <div className="bg-slate-900 border border-slate-800 rounded-[3rem] p-10">
        <div className="flex items-center gap-4 mb-8">
          <Building2 className="text-amber-500" size={32} />
          <h2 className="text-2xl font-black text-white italic uppercase tracking-tighter">Micropolix: Job Shadowing</h2>
        </div>
        
        {submitted ? (
          <div className="text-center py-10">
            <CheckCircle2 size={64} className="text-emerald-500 mx-auto mb-6" />
            <h3 className="text-2xl font-black text-white italic uppercase mb-2">Solicitud Enviada</h3>
            <p className="text-slate-400 mb-8">Hemos registrado tu interés. Te avisaremos en los próximos 15 días para coordinar tu jornada de inmersión técnica.</p>
            <button onClick={() => setSubmitted(false)} className="text-indigo-400 font-bold uppercase text-xs tracking-widest">Hacer otra solicitud</button>
          </div>
        ) : (
          <form onSubmit={(e) => { e.preventDefault(); setSubmitted(true); }} className="space-y-6">
            <div className="grid md:grid-cols-2 gap-6">
              <div>
                <label className="text-xs font-black text-slate-500 uppercase ml-2 mb-2 block">Área que quieres conocer</label>
                <select className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white outline-none focus:ring-2 focus:ring-amber-500 transition-all">
                  <option>Ingeniería de Procesos</option>
                  <option>Análisis de Datos</option>
                  <option>Gestión de Calidad</option>
                  <option>Marketing Estratégico</option>
                </select>
              </div>
              <div>
                <label className="text-xs font-black text-slate-500 uppercase ml-2 mb-2 block">Compañero Referente</label>
                <input type="text" required placeholder="Nombre de la persona" className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white outline-none focus:ring-2 focus:ring-amber-500 transition-all" />
              </div>
            </div>
            <div>
              <label className="text-xs font-black text-slate-500 uppercase ml-2 mb-2 block">¿Qué esperas aprender?</label>
              <textarea rows="4" className="w-full bg-slate-800 border border-slate-700 rounded-2xl px-4 py-3 text-white outline-none focus:ring-2 focus:ring-amber-500 transition-all" placeholder="Describe brevemente tus objetivos de aprendizaje..."></textarea>
            </div>
            <p className="text-[10px] text-slate-500 uppercase font-black tracking-widest mb-4">Nota: Actividad semestral enfocada en la integración y transferencia de conocimiento.</p>
            <button className="w-full bg-amber-500 hover:bg-amber-400 text-slate-950 font-black py-4 rounded-2xl shadow-lg transition-all uppercase tracking-widest text-sm">Enviar Solicitud Micropolix</button>
          </form>
        )}
      </div>
    </div>
  );
};

const BonosView = ({ coins, setCoins }) => {
  const bonuses = [
    { name: "50€ Extra Ticket Restaurante", cost: 1000, icon: <Utensils size={32} /> },
    { name: "Tarde de Viernes Libre", cost: 2000, icon: "🏖️" },
    { name: "Curso Especialización I+D", cost: 1500, icon: "🎓" },
    { name: "Bonificación 100€ Nómina", cost: 3500, icon: <Coins size={32} /> },
    { name: "Gadget Tecnológico", cost: 3000, icon: "🎧" },
    { name: "Suscripción Revista Científica", cost: 800, icon: "🔬" }
  ];

  const redeem = (cost) => {
    if(coins >= cost) {
      setCoins(p => p - cost);
    }
  };

  return (
    <div className="grid md:grid-cols-3 gap-6 animate-in fade-in slide-in-from-bottom-4">
      {bonuses.map((b, idx) => (
        <div key={idx} className="bg-slate-900 border border-slate-800 rounded-[2.5rem] p-6 text-center group hover:border-indigo-500/50 transition-all">
          <div className="text-5xl mb-4 group-hover:scale-110 transition-transform flex justify-center text-indigo-400">
            {typeof b.icon === 'string' ? b.icon : b.icon}
          </div>
          <h4 className="text-lg font-black text-white italic uppercase mb-2 leading-tight">{b.name}</h4>
          <div className="flex items-center justify-center gap-2 mb-6 text-amber-500">
            <Coins size={16} />
            <span className="font-black">{b.cost} Bio-Credits</span>
          </div>
          <button 
            onClick={() => redeem(b.cost)}
            disabled={coins < b.cost}
            className={`w-full py-3 rounded-xl font-black text-xs uppercase tracking-widest transition-all ${coins >= b.cost ? 'bg-indigo-600 text-white hover:bg-indigo-500 shadow-lg shadow-indigo-600/20' : 'bg-slate-800 text-slate-600 cursor-not-allowed'}`}
          >
            {coins >= b.cost ? 'Canjear Recompensa' : 'Bio-Credits insuficientes'}
          </button>
        </div>
      ))}
    </div>
  );
};

export default App;
