# Advance-tracing
Advanced Tracing &amp; Observability tracks prompts, decisions, tool calls, latency, errors, and task success in real time. Its Controlled Failure Lab injects failures, identifies root causes, and applies recovery strategies, showing measurable before-vs-after improvements.
Mamber name 1.gayatri autade 2.mansi wake 3.shruti dange.
Frontend: HTML, CSS, JavaScript
Backend: Python
AI Agent: LLM/API
Tracing: OpenTelemetry
Data Storage: SQLite
Visualization: Charts/Graphs
Testing: Automated evaluation & failure injection
import React, { useEffect, useState } from "react";
import {
  Activity,
  Bot,
  CheckCircle2,
  Clock,
  Wrench,
  AlertTriangle,
  Zap,
  Search,
  RefreshCw,
  ArrowDown,
  CircleDot,
  TrendingDown,
  TrendingUp,
} from "lucide-react";

type TraceEvent = {
  id: number;
  agent: string;
  action: string;
  type: "prompt" | "decision" | "tool" | "error" | "success";
  latency: string;
  tokens: number;
  status: "success" | "error" | "running";
};

export default function AdvancedTracing() {
  const [failureInjected, setFailureInjected] = useState(false);
  const [diagnosed, setDiagnosed] = useState(false);
  const [optimized, setOptimized] = useState(false);
  const [events, setEvents] = useState<TraceEvent[]>([
    {
      id: 1,
      agent: "Research Agent",
      action: "Received research prompt",
      type: "prompt",
      latency: "120ms",
      tokens: 142,
      status: "success",
    },
    {
      id: 2,
      agent: "Planning Agent",
      action: "Selected research strategy",
      type: "decision",
      latency: "84ms",
      tokens: 96,
      status: "success",
    },
    {
      id: 3,
      agent: "Search Agent",
      action: "Called market intelligence tool",
      type: "tool",
      latency: "1.2s",
      tokens: 220,
      status: "success",
    },
  ]);

  const injectFailure = () => {
    if (failureInjected) return;

    setFailureInjected(true);
    setDiagnosed(false);
    setOptimized(false);

    setEvents((prev) => [
      ...prev,
      {
        id: Date.now(),
        agent: "Search Agent",
        action: "Tool request failed: External API timeout",
        type: "error",
        latency: "5.0s",
        tokens: 0,
        status: "error",
      },
    ]);
  };

  const diagnoseFailure = () => {
    if (!failureInjected) return;

    setDiagnosed(true);

    setEvents((prev) => [
      ...prev,
      {
        id: Date.now(),
        agent: "Observability Agent",
        action:
          "Root cause identified: search API timeout exceeded configured threshold",
        type: "decision",
        latency: "210ms",
        tokens: 78,
        status: "success",
      },
    ]);
  };

  const optimizeSystem = () => {
    if (!diagnosed) return;

    setOptimized(true);

    setEvents((prev) => [
      ...prev,
      {
        id: Date.now(),
        agent: "Recovery Agent",
        action:
          "Applied fallback source and reduced retry strategy automatically",
        type: "success",
        latency: "740ms",
        tokens: 54,
        status: "success",
      },
      {
        id: Date.now() + 1,
        agent: "IntelAgent",
        action: "Task recovered successfully and execution completed",
        type: "success",
        latency: "2.1s",
        tokens: 310,
        status: "success",
      },
    ]);
  };

  const getIcon = (type: TraceEvent["type"]) => {
    switch (type) {
      case "prompt":
        return <Bot size={18} />;
      case "decision":
        return <CircleDot size={18} />;
      case "tool":
        return <Wrench size={18} />;
      case "error":
        return <AlertTriangle size={18} />;
      case "success":
        return <CheckCircle2 size={18} />;
    }
  };

  return (
    <section className="space-y-6 py-8">
      {/* HEADER */}
      <div className="rounded-3xl border border-slate-200 bg-white p-6 shadow-sm">
        <div className="flex items-center gap-3">
          <div className="rounded-2xl bg-teal-50 p-3 text-teal-700">
            <Activity size={26} />
          </div>

          <div>
            <p className="text-xs font-bold tracking-[0.3em] text-teal-700">
              ADVANCED OBSERVABILITY
            </p>
            <h2 className="mt-2 text-3xl font-bold text-slate-900">
              See how every decision happens.
            </h2>
            <p className="mt-2 text-slate-500">
              Trace agents, prompts, decisions, tools, latency, tokens, and
              failures from start to finish.
            </p>
          </div>
        </div>
      </div>

      {/* METRICS */}
      <div className="grid grid-cols-2 gap-4 md:grid-cols-4">
        <MetricCard
          icon={<Clock size={20} />}
          label="AVG LATENCY"
          value={optimized ? "2.1s" : "3.8s"}
          improvement={optimized ? "45% faster" : "Baseline"}
        />

        <MetricCard
          icon={<Wrench size={20} />}
          label="TOOL CALLS"
          value={optimized ? "8" : "14"}
          improvement={optimized ? "43% fewer" : "Baseline"}
        />

        <MetricCard
          icon={<AlertTriangle size={20} />}
          label="ERRORS"
          value={optimized ? "1" : "4"}
          improvement={optimized ? "75% reduced" : "Before optimization"}
        />

        <MetricCard
          icon={<CheckCircle2 size={20} />}
          label="TASK SUCCESS"
          value={optimized ? "96%" : "78%"}
          improvement={optimized ? "+18% improvement" : "Baseline"}
        />
      </div>

      {/* FAILURE LAB */}
      <div className="rounded-3xl border border-slate-200 bg-slate-950 p-6 text-white shadow-sm">
        <div className="flex items-start justify-between gap-4">
          <div>
            <p className="text-xs font-bold tracking-[0.3em] text-amber-400">
              CONTROLLED FAILURE LAB
            </p>

            <h3 className="mt-2 text-2xl font-bold">
              Break it. Trace it. Improve it.
            </h3>

            <p className="mt-2 max-w-2xl text-slate-400">
              Introduce a controlled tool failure and allow IntelAgent to
              identify the root cause, diagnose the problem, and automatically
              recover.
            </p>
          </div>

          <Zap className="text-amber-400" size={30} />
        </div>

        <div className="mt-6 grid gap-3 md:grid-cols-3">
          <button
            onClick={injectFailure}
            className="rounded-xl border border-red-400/30 bg-red-500/10 p-4 text-left transition hover:bg-red-500/20"
          >
            <AlertTriangle className="mb-2 text-red-400" />
            <p className="font-semibold">1. Inject Failure</p>
            <p className="mt-1 text-sm text-slate-400">
              Simulate an external API timeout.
            </p>
          </button>

          <button
            onClick={diagnoseFailure}
            disabled={!failureInjected}
            className="rounded-xl border border-amber-400/30 bg-amber-500/10 p-4 text-left transition hover:bg-amber-500/20 disabled:cursor-not-allowed disabled:opacity-40"
          >
            <Search className="mb-2 text-amber-400" />
            <p className="font-semibold">2. Diagnose Root Cause</p>
            <p className="mt-1 text-sm text-slate-400">
              Analyze traces and identify failure.
            </p>
          </button>

          <button
            onClick={optimizeSystem}
            disabled={!diagnosed}
            className="rounded-xl border border-teal-400/30 bg-teal-500/10 p-4 text-left transition hover:bg-teal-500/20 disabled:cursor-not-allowed disabled:opacity-40"
          >
            <RefreshCw className="mb-2 text-teal-400" />
            <p className="font-semibold">3. Recover & Improve</p>
            <p className="mt-1 text-sm text-slate-400">
              Apply fallback and optimize execution.
            </p>
          </button>
        </div>
      </div>

      {/* TRACE TIMELINE */}
      <div className="rounded-3xl border border-slate-200 bg-white p-6 shadow-sm">
        <div className="mb-6">
          <p className="text-xs font-bold tracking-[0.3em] text-teal-700">
            END-TO-END TRACE
          </p>
          <h3 className="mt-2 text-2xl font-bold text-slate-900">
            Every step leaves a receipt
          </h3>
        </div>

        <div className="space-y-3">
          {events.map((event) => (
            <div
              key={event.id}
              className={`flex items-center gap-4 rounded-2xl border p-4 ${
                event.status === "error"
                  ? "border-red-200 bg-red-50"
                  : event.status === "success"
                  ? "border-slate-100 bg-slate-50"
                  : "border-amber-200 bg-amber-50"
              }`}
            >
              <div
                className={`rounded-xl p-3 ${
                  event.status === "error"
                    ? "bg-red-100 text-red-600"
                    : "bg-teal-100 text-teal-700"
                }`}
              >
                {getIcon(event.type)}
              </div>

              <div className="flex-1">
                <p className="font-semibold text-slate-800">
                  {event.agent}
                </p>
                <p className="text-sm text-slate-500">{event.action}</p>
              </div>

              <div className="hidden text-right
