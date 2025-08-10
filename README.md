// Projeto: enem-2025
// Repositório sugerido: https://github.com/seu-usuario/enem-2025
// Deploy: https://enem-2025.vercel.app

import React, { useState } from 'react';
import { Tabs, TabsList, TabsTrigger, TabsContent } from './components/ui/tabs';
import { Button } from './components/ui/button';
import { Sheet, SheetContent, SheetTrigger, SheetHeader, SheetTitle } from './components/ui/sheet';
import { Calendar, PenTool, Target, TrendingUp, FileText, Mail, BookOpen, Menu } from 'lucide-react';

export default function App() {
  const [activeTab, setActiveTab] = useState('cronograma');
  const [isMenuOpen, setIsMenuOpen] = useState(false);

  const tabs = [
    { value: 'cronograma', label: 'Cronograma', icon: Calendar },
    { value: 'redacao', label: 'Redação', icon: PenTool },
    { value: 'dicas', label: 'Dicas', icon: Target },
    { value: 'atualidades', label: 'Atualidades', icon: TrendingUp },
    { value: 'simulados', label: 'Simulados', icon: FileText },
    { value: 'contato', label: 'Contato', icon: Mail }
  ];

  const handleTabChange = (value: string) => {
    setActiveTab(value);
    setIsMenuOpen(false);
  };

  const renderTabContent = (tab: string) => {
    switch (tab) {
      case 'cronograma':
        return <div className="text-white text-xl">📅 Aqui vai seu cronograma de estudos...</div>;
      case 'redacao':
        return <div className="text-white text-xl">✍️ Área para enviar e corrigir redações.</div>;
      case 'dicas':
        return <div className="text-white text-xl">🎯 Dicas estratégicas para o ENEM.</div>;
      case 'atualidades':
        return <div className="text-white text-xl">📈 Temas importantes e atualizados.</div>;
      case 'simulados':
        return <div className="text-white text-xl">📝 Simulados para praticar.</div>;
      case 'contato':
        return (
          <div className="text-white text-xl space-y-4 text-center">
            <Mail className="mx-auto" size={48} />
            <p>Precisa de ajuda? Entre em contato!</p>
            <Button className="bg-white text-purple-900 hover:bg-purple-100">Instruções de hospedagem</Button>
            <Button variant="outline" className="border-white/30 text-white hover:bg-white/10">
              Baixar arquivos
            </Button>
          </div>
        );
      default:
        return null;
    }
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-purple-900 via-violet-800 to-indigo-900 relative overflow-hidden">
      <div className="absolute inset-0 opacity-10">
        <div className="absolute top-20 left-10 w-32 h-32 bg-white/20 rounded-full blur-2xl"></div>
        <div className="absolute top-40 right-20 w-48 h-48 bg-pink-300/20 rounded-full blur-3xl"></div>
        <div className="absolute bottom-20 left-20 w-40 h-40 bg-blue-300/20 rounded-full blur-2xl"></div>
        <div className="absolute bottom-40 right-10 w-56 h-56 bg-purple-300/20 rounded-full blur-3xl"></div>
      </div>

      <a href="#main-content" className="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4 bg-white text-purple-900 px-4 py-2 rounded-lg z-50 font-medium">
        Pular para conteúdo principal
      </a>

      <header className="relative z-10 backdrop-blur-md bg-white/10 border-b border-white/20">
        <div className="max-w-7xl mx-auto px-4 py-6 sm:py-12 text-center space-y-6">
          <div className="flex items-center justify-center gap-4">
            <div className="bg-white/20 p-4 rounded-2xl border border-white/30">
              <BookOpen size={36} className="text-white" />
            </div>
            <div>
              <h1 className="text-4xl sm:text-5xl font-bold text-white">ENEM 2025</h1>
              <p className="text-xl text-purple-100">Seu guia completo de estudos</p>
            </div>
          </div>
          <p className="text-purple-100 max-w-3xl mx-auto text-lg leading-relaxed">
            Cronograma, redação, simulados, dicas e muito mais para garantir sua vaga na universidade!
          </p>
        </div>
      </header>

      <main className="relative z-10 max-w-7xl mx-auto px-4 py-6 sm:py-8" id="main-content">
        <Tabs value={activeTab} onValueChange={setActiveTab} className="w-full">
          <TabsList className="hidden md:grid grid-cols-6 bg-white/20 backdrop-blur-md border border-white/30 rounded-2xl mb-6 p-2">
            {tabs.map(({ value, label, icon: Icon }) => (
              <TabsTrigger
                key={value}
                value={value}
                className="flex items-center gap-2 py-3 px-4 text-white data-[state=active]:bg-white data-[state=active]:text-purple-900 rounded-xl transition-all duration-300 hover:bg-white/10"
              >
                <Icon size={18} />
                <span>{label}</span>
              </TabsTrigger>
            ))}
          </TabsList>

          <div className="md:hidden mb-6">
            <Sheet open={isMenuOpen} onOpenChange={setIsMenuOpen}>
              <SheetTrigger asChild>
                <Button variant="ghost" className="w-full justify-between px-4 py-3 text-white bg-white/10 rounded-xl">
                  <div className="flex items-center gap-3">
                    {(() => {
                      const currentTab = tabs.find(t => t.value === activeTab);
                      const Icon = currentTab?.icon || Calendar;
                      return (
                        <>
                          <Icon size={20} />
                          <span>{currentTab?.label || 'Menu'}</span>
                        </>
                      );
                    })()}
                  </div>
                  <Menu size={20} />
                </Button>
              </SheetTrigger>
              <SheetContent side="bottom" className="h-auto max-h-[80vh] bg-white/95 rounded-t-2xl p-4">
                <SheetHeader className="mb-4">
                  <SheetTitle className="text-purple-900">Navegação</SheetTitle>
                </SheetHeader>
                <div className="grid grid-cols-2 gap-4">
                  {tabs.map(({ value, label, icon: Icon }) => (
                    <Button
                      key={value}
                      variant={activeTab === value ? 'default' : 'outline'}
                      className={`flex flex-col gap-2 h-20 ${activeTab === value ? 'bg-purple-900 text-white' : 'text-purple-900 border-purple-300'}`}
                      onClick={() => handleTabChange(value)}
                    >
                      <Icon size={22} />
                      <span className="text-sm">{label}</span>
                    </Button>
                  ))}
                </div>
              </SheetContent>
            </Sheet>
          </div>

          {tabs.map(({ value }) => (
            <TabsContent key={value} value={value}>
              <div className="bg-white/10 rounded-2xl p-6 border border-white/30 backdrop-blur-md min-h-[300px]">
                {renderTabContent(value)}
              </div>
            </TabsContent>
          ))}
        </Tabs>
      </main>
    </div>
  );
}
